# Unit 3: Multi-Agent Design & Building the Workflow

[← Back to course overview](../README.md)

## Learning Objectives

Learn to use n8n to wire multiple specialized agents into a single workflow that triages and hands off correctly.

## Accounts to Set Up

- **n8n Cloud**: 14-day free trial; continuing past that requires a paid plan (exact plan and pricing to be checked at the time)

## Background Knowledge Needed

- **What a Webhook is**: how n8n receives an external trigger
- **Conditional logic/flow control**: Switch/Set nodes are really just if-else under the hood
- **Calling a REST API to query a database**: hooking up to the Supabase instance built in Unit 2

## Class Content

- Sign up for n8n Cloud, tour the environment and interface
- Side-by-side comparison: n8n's Embeddings/Vector Store nodes do exactly what was done by hand with Postman/curl last unit — the node is a shell, not a black box
- Review from last session, Q&A
- Multi-agent architecture design: why split into multiple agents (intent triage, technical support, billing support)
- Build the intent-triage skeleton using n8n's Switch/Set nodes
- Assign each sub-agent its own Context and Tool (e.g. the billing agent queries the Supabase table built in Unit 2 via an n8n node)
- Wire up the full multi-agent workflow and test a simple case to confirm handoff works smoothly

### 90-Minute Rundown

| Time | Content |
| --- | --- |
| 0:00–0:10 | Sign up for n8n Cloud, tour the environment and interface |
| 0:10–0:20 | Compare n8n nodes to last unit's hand-built API calls: the Embeddings/Vector Store nodes make the same calls |
| 0:20–0:40 | Multi-agent architecture design: why split into multiple agents, customer-service flow design methodology |
| 0:40–1:00 | Build the intent-triage skeleton with Switch/Set nodes |
| 1:00–1:20 | Assign each sub-agent its Context and Tool (the billing agent queries the Supabase table from Unit 2), wire up the full workflow |
| 1:20–1:30 | Test cross-agent handoff, assign homework |

## Deliverables

A working multi-agent workflow in n8n (intent triage + wired-up RAG node + a billing agent that can successfully query the fake Supabase data)

## Homework

_Not decided yet._

---

[← Previous: Building Context](unit-2.md) ｜ [Next: End-to-End Integration →](unit-4.md)
