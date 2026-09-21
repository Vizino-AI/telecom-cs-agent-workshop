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
| Unit 2 | Building the Agent's Eyes: Context (dynamic data via Supabase, hands-on; RAG covered conceptually, built next unit) | [units/unit-2.md](units/unit-2.md) |
| Unit 3 | Building the Agent's Brains and Hands: Multi-Agent Model Design, RAG Knowledge Base & Tool Wiring | [units/unit-3.md](units/unit-3.md) |
| Unit 4 | Completing the Agent's Hands and Feet: End-to-End Tool Integration (web front end, backend, logging) | [units/unit-4.md](units/unit-4.md) |
| Unit 5 | Hardening the Agent's Model, Context & Tool: Guardrails, Evaluation & Reliability | [units/unit-5.md](units/unit-5.md) |

## Other Documents

- [scenarios.md](scenarios.md) — three core customer-service scenarios used as reference for fake data and demos
- [architecture.md](architecture.md) — service flow design, human-in-the-loop, and the three-channel front-end rollout
- [tools.md](tools.md) — every tool's purpose, why it was chosen, and its pricing tier

## Tech Stack at a Glance

- Core automation platform: n8n Cloud
- Language models
- Embedding: Voyage AI (Anthropic's official recommended partner)
- Vector database: TBD
- Dynamic data: Supabase
- Conversational front end: n8n Hosted Chat (built-in Chat Trigger node)
- Human-in-the-loop: Slack
- Tooling: Postman, Github, Git, Visual Studio Code

See [tools.md](tools.md) for the reasoning behind each choice.

## Note for Claude Code

Read [`CLAUDE.md`](CLAUDE.md) before doing anything related to this workshop.
