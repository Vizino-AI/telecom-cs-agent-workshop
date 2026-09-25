# Blazz Telecom Customer Service AI Agent Workshop

A five-unit, hands-on workshop: skip the theory behind generative AI and agentic AI, and go straight to building a multi-agent AI customer-service system for a realistic telecom scenario (fictional carrier **Blazz**) — so the student walks away with the satisfaction of having shipped something real.

## Goals & Framing

- Audience: a student who already has some AI coursework under their belt and wants to skip the theory and build something real
- Teaching approach: skip the fundamentals of generative AI and agentic AI, go straight to hands-on implementation
- Deliverable: a "telecom customer-service AI agent (multi-agent)" close to a real business need
- Core value: the satisfaction of shipping a real, working product

## Fictional Setting

- Carrier: **Blazz**
- AI agent's persona name: **Blake** (in the chat front end and every scenario example, the agent talks to customers as "Blake")

## Course Overview

Five units, ~90 minutes each. Each unit's full detail (learning objectives, setup, background knowledge, timed class content, deliverables, homework) lives in its own file:

| Unit | Topic | Link |
| --- | --- | --- |
| Unit 1 | The Three Pillars of an Agent: Model (Brain), Context (Eyes), Tool (Hands & Feet) | [units/unit-1.md](units/unit-1.md) |
| Unit 2 | Blazz's First Working Bot: Context, Memory & Tool Calling — Scenario 1, built hands-on in n8n | [units/unit-2.md](units/unit-2.md) |
| Unit 3 | Completing All Three Scenarios: Tool Wiring & Human-in-the-Loop (Slack + Email) | [units/unit-3.md](units/unit-3.md) |
| Unit 4 | One Agent, Three Scenarios: Front-Desk Triage, Confidence Fallback & Embedded Chat | [units/unit-4.md](units/unit-4.md) |
| Unit 5 | Hardening the Agent's Model, Context & Tool: Guardrails, Evaluation & Reliability | [units/unit-5.md](units/unit-5.md) |

## Other Documents

- [scenarios.md](scenarios.md) — three core customer-service scenarios used as reference for fake data and demos
- [architecture.md](architecture.md) — service flow design, human-in-the-loop, and the web front-end design
- [tools.md](tools.md) — every tool's purpose, why it was chosen, and its pricing tier

## Tech Stack at a Glance

- Core automation platform: n8n Cloud
- Language models
- Dynamic data: Supabase
- Conversational front end: n8n Chat Trigger (Hosted Chat in Unit 2 → Embedded Chat on a custom page in Unit 4)
- Human-in-the-loop: Slack + Email
- Tooling: Github, Git, Visual Studio Code

See [tools.md](tools.md) for the reasoning behind each choice.

## Note for Claude Code

Read [`CLAUDE.md`](CLAUDE.md) before doing anything related to this workshop.
