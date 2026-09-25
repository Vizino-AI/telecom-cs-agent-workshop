# Migrating Self-Hosted n8n: GCP → Hostinger

> Personal setup notes — for handing the n8n instance off from the instructor's GCP box to the student's own Hostinger account. Not part of the student curriculum (see [`../tools.md`](../tools.md)). Companion to [`n8n-on-gcp.md`](n8n-on-gcp.md) — read that first; this doc reuses its Docker Compose + Caddy setup on the new box.

Method: **export/import via n8n's CLI** (workflows + credentials as JSON), not a raw volume copy.

**Trade-off, on purpose**: this loses execution history (past run logs stay on GCP only) and the owner-account login doesn't come across either — you set a fresh one on Hostinger. In exchange, you don't need to match `N8N_ENCRYPTION_KEY` between the two servers, which makes this the simpler, good-enough-for-a-workshop-handoff option. If execution history or a zero-downtime cutover ever matters, do a volume copy instead (tar up the `n8n_data` Docker volume and restore it on the new box, carrying the same encryption key across) — not covered here.

## Prerequisites

- The GCP instance (source) still up and reachable, per [`n8n-on-gcp.md`](n8n-on-gcp.md)
- A Hostinger **VPS** plan (not shared/web hosting — needs root SSH and the ability to run Docker)
- (Optional) the student's own domain, if not reusing the instructor's

## 1. Stand up a fresh n8n on Hostinger

SSH into the new Hostinger VPS and follow [`n8n-on-gcp.md`](n8n-on-gcp.md)'s Steps 4 and 6–8 there instead of on GCP: install Docker, write the same `docker-compose.yml` + `Caddyfile` (pointed at Hostinger's IP or the student's own domain), `docker compose up -d`.

This new instance gets its **own fresh `N8N_ENCRYPTION_KEY`** — no need to match the GCP one for this method, just set one and keep it (same warning as the GCP doc: don't let it auto-generate).

Open the new instance in a browser and complete the first-run **owner account setup** (email + password) before continuing — the CLI import steps below need an already-initialized instance to import into.

## 2. Export workflows + credentials from the GCP instance

On the GCP VM:

```bash
cd ~/n8n
docker compose exec n8n n8n export:workflow --all --output=/tmp/workflows.json
docker compose exec n8n n8n export:credentials --all --decrypted --output=/tmp/credentials.json
docker cp "$(docker compose ps -q n8n)":/tmp/workflows.json ./workflows.json
docker cp "$(docker compose ps -q n8n)":/tmp/credentials.json ./credentials.json
```

> ⚠️ **`--decrypted` means the credentials file is plaintext** — API keys, DB passwords, everything, readable by anyone who gets the file. That's what makes this method simple (no encryption-key juggling), but treat `credentials.json` like the secrets it contains: transfer it only over `scp` (already encrypted in transit), and delete every copy the moment the import succeeds (Step 5).

## 3. Transfer the export files to Hostinger

From the GCP VM (or your own machine, if you downloaded them there first):

```bash
scp workflows.json credentials.json user@<hostinger-ip>:~/n8n/
```

## 4. Import on Hostinger

On the Hostinger VPS:

```bash
cd ~/n8n
docker cp ./workflows.json "$(docker compose ps -q n8n)":/tmp/workflows.json
docker cp ./credentials.json "$(docker compose ps -q n8n)":/tmp/credentials.json
docker compose exec n8n n8n import:workflow --input=/tmp/workflows.json
docker compose exec n8n n8n import:credentials --input=/tmp/credentials.json
```

Open the n8n UI and spot-check: workflows are all present, and a credential (e.g. the Supabase connection) opens without an error.

## 5. Clean up the plaintext credentials file — everywhere

```bash
# GCP VM
rm ~/n8n/workflows.json ~/n8n/credentials.json
docker compose exec n8n rm /tmp/workflows.json /tmp/credentials.json

# Hostinger VPS
rm ~/n8n/workflows.json ~/n8n/credentials.json
docker compose exec n8n rm /tmp/workflows.json /tmp/credentials.json

# wherever scp was run from, if a copy landed there too
```

## 6. Point DNS at the new server

Update the domain's DNS A record to the Hostinger VPS's IP (same Cloudflare "DNS only" / grey-cloud requirement as the GCP doc's Step 5 — a proxied record breaks Caddy's HTTPS cert request). Caddy on the new box will auto-request its own Let's Encrypt certificate once DNS resolves to it.

If the student is moving to their **own domain** rather than reusing the instructor's, update `N8N_HOST`/`WEBHOOK_URL` in Hostinger's `docker-compose.yml` and the hostname in its `Caddyfile` to match (see the GCP doc's "Changing the domain later" section for the exact recreate steps) — and update any embedded-chat pages (e.g. the Unit 4 HTML page) that reference the old webhook URL.

## 7. Verify, then decommission GCP

Test the full flow end to end on the new instance (chat trigger, tool calls, Slack/email escalation) before tearing anything down. Once confirmed:

```bash
gcloud compute instances delete n8n-server --zone=$GCP_ZONE
```

It's on the Always Free tier, so leaving it running costs nothing — but an unused, unmaintained instance is still worth cleaning up.

## What doesn't come across

- **Execution history** — past workflow runs/logs stay on the GCP instance only
- **The owner account** — login email/password is separate from workflow credentials; set fresh in Step 1
