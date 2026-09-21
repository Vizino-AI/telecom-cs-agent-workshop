# Self-Hosting n8n on GCP (Free Tier, 24/7)

> Personal setup notes — for the instructor's own free/always-on n8n instance. Not part of the student curriculum (see [`../tools.md`](../tools.md), which deliberately keeps the student-facing stack on n8n Cloud / cloud-first, no self-hosting).

Stack: **GCP Compute Engine (e2-micro, Always Free) + Docker + Caddy (automatic HTTPS)**.

**Current deployment**: `n8n.vizino.ai` → static IP `34.24.24.165` (VM `n8n-server`, zone `us-east1-b`), DNS on Cloudflare set to DNS-only. Project ID/billing account are in [`../.env`](../.env).

## Prerequisites
- A GCP account with billing enabled (Always Free still requires a card on file, but you won't be charged as long as you stay within the free-tier limits)
- Recommended: set a Budget Alert (e.g. $5) under **Billing → Budgets & alerts** as a safety net
- A domain name (optional but strongly recommended — a cheap one from Namecheap/Cloudflare Registrar works fine). No domain? See the nip.io alternative in Step 5.

All commands below are meant to be run in **Cloud Shell or your own terminal** with the `gcloud` CLI authenticated to your account — not inside this project's dev environment.

Actual project ID and billing account ID are secrets and live in [`../.env`](../.env), not in this doc. Export them into your shell first:

```bash
export GCP_PROJECT_ID=<value from ../.env>
export GCP_BILLING_ACCOUNT_ID=<value from ../.env>
export GCP_ZONE=us-east1-b
export GCP_REGION=us-east1
```

## 0. Create the GCP project and link billing

```bash
gcloud projects create $GCP_PROJECT_ID --name="n8n Playground"
gcloud config set project $GCP_PROJECT_ID
gcloud billing projects link $GCP_PROJECT_ID --billing-account=$GCP_BILLING_ACCOUNT_ID
gcloud services enable compute.googleapis.com --project=$GCP_PROJECT_ID
```

> ⚠️ **Project ID vs. project name**: if your preferred ID (e.g. `n8n-playground`) is already taken globally, GCP/the Console silently assigns a different auto-generated ID (e.g. `n8n-bot-487722`) while keeping your chosen string only as the *display name*. Every `gcloud` command needs the real **Project ID** — check with `gcloud projects list` if a command says a project "does not exist" even though you just created it.
>
> **Billing quota**: personal billing accounts default to a quota of 5 linked projects. If linking fails with `Cloud billing quota exceeded`, check what's already linked (`gcloud billing projects describe <PROJECT_ID>` for each) and unlink ones you don't need (`gcloud billing projects unlink <PROJECT_ID>`) rather than requesting a quota increase, which goes through a Google review queue.

## 1. Create the free VM (e2-micro)

Always Free rules: **one e2-micro instance per billing account**, and it must be in one of `us-west1`, `us-central1`, or `us-east1`.

```bash
gcloud compute instances create n8n-server \
  --zone=$GCP_ZONE \
  --machine-type=e2-micro \
  --image-family=ubuntu-2204-lts \
  --image-project=ubuntu-os-cloud \
  --boot-disk-size=30GB \
  --tags=http-server,https-server
```

> ⚠️ **First boot is CPU-heavy**: on first startup, n8n runs its full database migration history (hundreds of migrations on current versions), which is single-threaded and CPU-bound. On e2-micro's fractional vCPU this can take a very long time and even trigger SSH/instance instability under the load. If first boot seems stuck (no new log output, `uptime` shows a high load average), temporarily resize up, let migrations finish, then resize back down — this only costs a few cents:
> ```bash
> gcloud compute instances stop n8n-server --zone=$GCP_ZONE
> gcloud compute instances set-machine-type n8n-server --zone=$GCP_ZONE --machine-type=e2-small
> gcloud compute instances start n8n-server --zone=$GCP_ZONE
> # ...wait for migrations to finish (check: docker logs <n8n-container> --tail 20)...
> gcloud compute instances stop n8n-server --zone=$GCP_ZONE
> gcloud compute instances set-machine-type n8n-server --zone=$GCP_ZONE --machine-type=e2-micro
> gcloud compute instances start n8n-server --zone=$GCP_ZONE
> ```
> If the VM is forcibly stopped mid-migration, the SQLite WAL file can end up in a stuck/locked state, causing an infinite "Database ping failed" loop on next boot with no further progress. If that happens, don't delete the old volume (it may still be recoverable) — just point `docker-compose.yml` at a **new** volume name and recreate: `docker compose down && sed -i 's/n8n_data:/n8n_data_v2:/g' docker-compose.yml && docker compose up -d`. Safe to do before you've completed initial owner setup (nothing to lose yet).

## 2. Reserve a static external IP

Without this, the IP changes on every reboot and your domain's DNS record would break.

```bash
gcloud compute addresses create n8n-ip --region=$GCP_REGION
gcloud compute addresses describe n8n-ip --region=$GCP_REGION --format='get(address)'
```

Attach it to the VM:

```bash
gcloud compute instances delete-access-config n8n-server --zone=$GCP_ZONE --access-config-name="external-nat"
gcloud compute instances add-access-config n8n-server --zone=$GCP_ZONE --address=<the-ip-you-just-got>
```

> ⚠️ The access config name is case- and format-sensitive — it's `external-nat` (lowercase, hyphenated), not `External NAT`. Check the actual name first if unsure: `gcloud compute instances describe n8n-server --zone=$GCP_ZONE --format='get(networkInterfaces[0].accessConfigs[0].name)'`.

## 3. Open the firewall (80/443)

```bash
gcloud compute firewall-rules create allow-http-https \
  --allow=tcp:80,tcp:443 \
  --target-tags=http-server,https-server \
  --direction=INGRESS
```

## 4. SSH in and install Docker

```bash
gcloud compute ssh n8n-server --zone=$GCP_ZONE
```

Once inside the VM:

```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
exit
```

(SSH back in once more so the group change takes effect.)

## 5. Point a domain at the VM

Set your domain's A record to the static IP from Step 2, e.g. `n8n.yourdomain.com → 34.123.45.67`.

**No domain? Use [nip.io](https://nip.io)** — it turns any IP into a working hostname for free, e.g. IP `34.123.45.67` becomes `34-123-45-67.nip.io`. Caddy can issue a free HTTPS certificate for this just like a real domain, no purchase needed.

> ⚠️ **If your domain's DNS is on Cloudflare**, the record must be set to "DNS only" (grey cloud), not "Proxied" (orange cloud). A proxied record resolves to Cloudflare's edge IP instead of your VM, which breaks Caddy's Let's Encrypt HTTP-01 challenge (it needs to reach your VM directly). Toggle this in the Cloudflare dashboard next to the DNS record. Verify with `dig @1.1.1.1 +short yourdomain.com` — it should return your VM's static IP, not a `172.64.x.x`/`104.x.x.x` Cloudflare IP. (Your terminal's own DNS cache can lag behind the real change — always verify against a public resolver directly, not your default one.)

## 6. Write the docker-compose file

On the VM:

```bash
mkdir ~/n8n && cd ~/n8n
```

`docker-compose.yml`:
```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    environment:
      - N8N_HOST=n8n.yourdomain.com
      - N8N_PROTOCOL=https
      - WEBHOOK_URL=https://n8n.yourdomain.com/
      - GENERIC_TIMEZONE=America/Toronto
      - N8N_ENCRYPTION_KEY=generate-a-random-string-and-keep-it-fixed
    volumes:
      - n8n_data:/home/node/.n8n
    expose:
      - "5678"

  caddy:
    image: caddy:2
    restart: always
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile
      - caddy_data:/data
    depends_on:
      - n8n

volumes:
  n8n_data:
  caddy_data:
```

`Caddyfile` (use your real domain, or the nip.io one):
```
n8n.yourdomain.com {
    reverse_proxy n8n:5678
}
```

> ⚠️ Set `N8N_ENCRYPTION_KEY` explicitly (e.g. via `openssl rand -hex 24`) and keep it saved somewhere safe — don't let n8n auto-generate it. If you ever rebuild the machine, this key plus a backup of the data volume is what lets you decrypt stored credentials again.

## 7. Start it up

```bash
docker compose up -d
```

Give it a minute or two (Caddy needs to request the certificate from Let's Encrypt), then open `https://n8n.yourdomain.com` in a browser. On first load, n8n will ask you to set up the owner account and password.

## 8. Make sure it survives reboots

`restart: always` handles container-level restarts. Also make sure Docker itself starts on boot:

```bash
sudo systemctl enable docker
```

This way, even if GCP reboots the VM for routine maintenance, Docker starts → containers start → n8n is back up automatically, giving you real 24/7 uptime.

> ⚠️ **Add swap on e2-micro**: 1GB RAM with zero swap is tight for n8n's steady-state footprint (task runner subprocess, sandbox, etc.), and can cause the app to flap/restart internally right after a successful cold start. A free, non-destructive fix — add a 2GB swapfile (persists across reboots via `/etc/fstab`):
> ```bash
> sudo fallocate -l 2G /swapfile
> sudo chmod 600 /swapfile
> sudo mkswap /swapfile
> sudo swapon /swapfile
> echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab
> ```

### Changing the domain later

If you switch domains (e.g. from nip.io to a real one), update **both** `N8N_HOST`/`WEBHOOK_URL` in `docker-compose.yml` and the hostname in `Caddyfile`, then:
```bash
docker compose up -d        # recreates n8n (env var change needs this)
docker compose restart caddy  # full restart, not just reload
```
`caddy reload` can report "config is unchanged" and silently keep serving the old domain even after the Caddyfile content changed on disk — a full container restart reliably re-reads it from scratch.

## 9. Backups and cost monitoring

- **Backups**: periodically snapshot the boot disk (`gcloud compute disks snapshot`). Snapshots aren't part of the free tier but cost very little (billed per GB).
- **Free-tier limits to watch**: outbound network egress is free only up to 1GB/month (North America). Workshop-scale usage shouldn't come close, but keep an eye on billing.
- e2-micro has only 1GB RAM and a shared vCPU. Fine for normal n8n workflow use; if you're running heavy concurrent RAG/embedding calls and it feels sluggish, the next step up is `e2-small` (not free, ~$7/month).

## 10. The chat interface

n8n's own Chat Trigger node (Hosted Chat mode) serves the chat UI directly at a URL shaped like `https://n8n.yourdomain.com/webhook/xxx/chat` — identical in shape to what you'd get from n8n Cloud, just served from your own domain. No separate front-end tool needed.

---

Once set up, this is a genuinely free, always-on n8n instance. If the maintenance burden (OS updates, certificate renewal, occasional VM hiccups) ever outweighs the savings, workflows exported as JSON move over to n8n Cloud without any changes needed.
