# Project: Blazz Telecom Customer Service AI Agent Workshop

## Background

A one-on-one workshop: teach a student to build, from scratch, a multi-agent AI customer-service system for a realistic telecom scenario (fictional carrier **Blazz**).

Read [`README.md`](./README.md) first. Each unit's timed class content, setup, background knowledge, deliverables, and homework live under [`units/`](./units/); architecture and flow diagrams are in [`architecture.md`](./architecture.md); the three core scenarios are in [`scenarios.md`](./scenarios.md); tool choices and reasoning are in [`tools.md`](./tools.md).

This is a reusable template — keep student references generic ("the student"), not a specific name.

## Tech Stack

- Automation: **n8n Cloud** (no-code), account opened starting Unit 2
- Language models: **Gemini Flash** + **Gemini Pro**
- Conversational front end: **n8n Chat Trigger** — web only, Hosted Chat mode built in Unit 2, switched to Embedded Chat on a custom HTML page in Unit 4
- Dynamic data: **Supabase** (managed Postgres), plus **Supabase Storage** for reference documents (Unit 3)
- Human-in-the-loop: **Slack** + **Email**
- Dev assistance: Claude Code, kept to a no-code-friendly level

See [`tools.md`](./tools.md) for why each tool was chosen.

## Fictional Setting

- Carrier: **Blazz**
- AI agent's persona name: **Blake**
- Three core scenarios (see [`scenarios.md`](./scenarios.md)): billing inquiry & upsell, outage troubleshooting, cancellation & retention

## Reminders for Claude Code

- This is a **teaching project**: keep fake data, n8n workflow examples, and prompt drafts simple enough to build live with the student — don't over-engineer
- Keep `README.md` / `units/*.md` / `architecture.md` / `scenarios.md` / `tools.md` consistent with each other when you change the curriculum
- Homework is set per unit in each `units/*.md` file — don't invent or change it unless asked
- Confirm with Katness before changing price, session count, or scheduling
