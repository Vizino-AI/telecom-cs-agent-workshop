# Project: Blazz Telecom Customer Service AI Agent Workshop

## Background

This is a one-on-one workshop designed by Katness: teach a student to build, from scratch, a multi-agent AI customer-service system for a realistic telecom scenario (fictional carrier **Blazz**).

The course overview and framing live in [`README.md`](./README.md); each unit's 90-minute rundown, accounts to set up, background knowledge, deliverables, and homework are split one-file-per-unit under [`units/`](./units/); system architecture and flow diagrams are in [`architecture.md`](./architecture.md); the three core customer-service scenarios are in [`scenarios.md`](./scenarios.md); tool choices and pricing are in [`tools.md`](./tools.md). **Read `README.md` before doing anything related to this workshop.**

The student's real name, background, and commercial terms (price, number of sessions, actual session dates) live locally in `student.local.md` — this file is excluded via `.gitignore` and never committed or pushed. README / units / CLAUDE.md always refer to "the student" generically. **Never put the student's real name or identifying details into any file that gets committed.** When you need commercial terms or dates, read `student.local.md` (if it doesn't exist, ask Katness for it first).

Homework for each unit is intentionally left as "not decided yet" as of 2026-09-18 — don't invent homework content unless asked.

## Tech Stack & Conventions

- Core automation platform: **n8n Cloud** (no-code, uses built-in Webhook/OAuth, no self-hosted server) — free trial is only 14 days, so **the account isn't opened until Unit 3** (Units 1–2 never touch n8n, to avoid burning the trial early)
- Language models: **Claude 3.5 Sonnet** (high-logic workflows, intent classification, RAG response generation) + **GPT-4o** (collaboration/fallback)
- Conversational front end: **Voiceflow**, staged rollout — the web channel is built in Unit 4's class time; WhatsApp and phone are left as Unit 4 homework for the student to wire up on their own
- Vector database/RAG: **Qdrant** (or Pinecone) + **Voyage AI** (embedding, Anthropic's officially recommended partner — Anthropic doesn't offer its own embedding API, and the goal is to keep the stack inside the Anthropic ecosystem as much as possible); teaching deliberately **avoids making n8n the only path** — Unit 2 calls Voyage AI and Qdrant directly via Postman/curl first, so the student understands RAG is fundamentally just two independent HTTP APIs, and Unit 3 then shows that n8n's nodes are just a shell wrapping the same calls. Reasoning: n8n (and even Voiceflow) could be replaced by newer tools later, and we don't want the student to come away thinking "you can only query data through n8n"
- Dynamic data: **Supabase** (managed Postgres, free tier) — stores mutable data like billing/account status; teaching prefers managed/cloud services over self-hosting, consistent with the other tools (n8n Cloud, Qdrant Cloud, Voiceflow); the account and table are set up in Unit 2, and the billing agent queries it starting in Unit 3
- Human-in-the-loop: **Slack** (Blazz's internal support/engineering team)
- Dev assistance: Claude Code/Cursor — the goal is to preserve an overall **no-code build experience**; only reach for custom code when the student genuinely needs it, and avoid producing a pile of custom code they'd have to maintain afterward. Anything generated should be at a level the student can read and modify themselves
- Despite being billed as "no-code," some basic software-architecture knowledge is still required (API, HTTP/HTTPS, JSON, Webhooks, etc.) — every file under `units/` has a "Background Knowledge Needed" section; repeat a concept across units when it's used again

## Fictional Setting

- Carrier: **Blazz**
- AI agent's persona name: **Blake** (in the Voiceflow front end and every scenario example, the agent talks to customers as "Blake")
- Three core customer-service scenarios (see [`scenarios.md`](./scenarios.md)):
  1. Billing inquiry & plan upsell — API lookup + logical reasoning
  2. Internet outage troubleshooting — RAG + Slack human-in-the-loop
  3. Cancellation & retention — sentiment detection + retention offer + email
- Prefer these three scenarios when designing fake data, test cases, or demos

## Reminders for Claude Code

- This is a **teaching project**: fake data, n8n workflow examples, prompt drafts, etc. should be "simple enough to walk through and modify live with the student" — don't over-engineer or introduce frameworks they won't otherwise need
- When you change the curriculum, system design, or scenarios, update the corresponding file (`README.md` / `units/*.md` / `architecture.md` / `scenarios.md` / `tools.md`) so the documents don't drift out of sync with each other
- The content used to live in a single `cx-agent-planning.md`; on 2026-09-18 it was split into `README.md` + `units/` + `architecture.md` + `scenarios.md` + `tools.md`, translated to English, and renamed from "weeks" to "units" (a calendar week actually contains two sessions, so "week" was misleading); student identity and commercial terms moved to the git-ignored `student.local.md` so the repo can be published without exposing them
- Any change involving price, number of sessions, or scheduling needs Katness's sign-off first — and always goes into `student.local.md`, never into a committed file
