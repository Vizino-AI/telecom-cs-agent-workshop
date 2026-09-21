# Unit 3: Building the Agent's Brains and Hands — Multi-Agent Model Design & Tool Wiring

[← Back to course overview](../README.md)

## Learning Objectives

Learn to use n8n to wire multiple specialized agents into a single workflow that triages and hands off correctly, and build the RAG knowledge base using n8n's built-in nodes.

## Setup

- **n8n Cloud**: 14-day free trial; continuing past that requires a paid plan (exact plan and pricing to be checked at the time)
- **Qdrant Cloud**: free (free tier, permanent allowance)
- **Voyage AI**: new accounts usually get a free trial allowance; usage-based billing kicks in after that

## Nice to Know

- **What a Webhook is**: how n8n receives an external trigger
- **Conditional logic/flow control**: Switch/Set nodes are really just if-else under the hood
- **Calling a REST API to query a database**: hooking up to the Supabase instance built in Unit 2

## Class Content

- Sign up for n8n Cloud, Qdrant Cloud and Voyage AI; tour the n8n environment and interface; review from last session, Q&A (10 mins)
- **Build the RAG knowledge base with n8n's built-in nodes**: load Blazz's contracts/FAQs, embed them via the Embeddings node (Voyage AI, or the HTTP Request node if no dedicated node exists), and store them in the Vector Store node (Qdrant) — the node wraps the same kind of raw HTTP call the student made by hand for Supabase last unit, so it's a shell, not a black box (25 mins)
- Multi-agent architecture design: why split into multiple agents (intent triage, technical support, billing support) (10 mins)
- Build the intent-triage skeleton using n8n's Switch/Set nodes (20 mins)
- Assign each sub-agent its own Context and Tool (e.g. the technical-support agent queries the RAG node just built and fetches the matching device diagram from the Supabase Storage bucket built in Unit 2; the billing agent queries the Supabase table built in Unit 2 via an n8n node); wire up the full multi-agent workflow (20 mins)
- Test a simple case to confirm handoff works smoothly; wrap-up (5 mins)

## Deliverables

A working multi-agent workflow in n8n: intent triage, a technical-support agent backed by a newly built RAG knowledge base (Qdrant + Voyage AI via n8n nodes) plus the Unit 2 device-diagram Storage bucket, and a billing agent that can successfully query the fake Supabase table data

## Homework

TBD

---

[← Previous: Building the Agent's Eyes](unit-2.md) ｜ [Next: Completing the Agent's Hands and Feet →](unit-4.md)
