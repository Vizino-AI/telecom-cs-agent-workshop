# Unit 3: Building the Agent's Brains and Hands — Multi-Agent Model Design & Tool Wiring

[← Back to course overview](../README.md)

## Learning Objectives

Learn to use n8n to wire multiple specialized agents into a single workflow that triages and hands off correctly.

## Setup

- **n8n Cloud**: 14-day free trial; continuing past that requires a paid plan (exact plan and pricing to be checked at the time)

## Nice to Know

- **What a Webhook is**: how n8n receives an external trigger
- **Conditional logic/flow control**: Switch/Set nodes are really just if-else under the hood
- **Calling a REST API to query a database**: hooking up to the Supabase instance built in Unit 2

## Class Content

- Sign up for n8n Cloud, tour the environment and interface; review from last session, Q&A (10 mins)
- Side-by-side comparison: n8n's Embeddings/Vector Store nodes do exactly what was done by hand with Postman/curl last unit — the node is a shell, not a black box (10 mins)
- Multi-agent architecture design: why split into multiple agents (intent triage, technical support, billing support) (20 mins)
- Build the intent-triage skeleton using n8n's Switch/Set nodes (20 mins)
- Assign each sub-agent its own Context and Tool (e.g. the billing agent queries the Supabase table built in Unit 2 via an n8n node); wire up the full multi-agent workflow (20 mins)
- Test a simple case to confirm handoff works smoothly; wrap-up (10 mins)

## Deliverables

A working multi-agent workflow in n8n (intent triage + wired-up RAG node + a billing agent that can successfully query the fake Supabase data)

## Homework

TBD

---

[← Previous: Building the Agent's Eyes](unit-2.md) ｜ [Next: Completing the Agent's Hands and Feet →](unit-4.md)
