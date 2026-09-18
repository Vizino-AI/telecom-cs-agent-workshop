# Unit 2: Building Context

[← Back to course overview](../README.md)

## Learning Objectives

Understand Context's two faces — RAG for static knowledge, Supabase for dynamic data — and build both by calling raw APIs first, without n8n.

## Setup

- **Qdrant Cloud**: free (free tier, permanent allowance)
- **Voyage AI**: new accounts usually get a free trial allowance; usage-based billing kicks in after that
- **Supabase**: free tier (plenty for this course's scale); upgrading to paid only matters at higher usage or for more features
- Postman (optional): the free tier is enough; using curl instead means no account at all

## Background Knowledge Needed

- **HTTP basics**: request/response, methods (GET/POST), endpoints, headers, body
- **HTTPS and API key/Bearer token auth**: why an API call needs a key, and why data gets encrypted in transit
- **JSON**: the common language APIs speak
- **The concept of vectors/embeddings**: semantic search
- **Basic relational-database concepts**: tables, columns, rows (needed for Supabase)

## Class Content

- Review from last session, Q&A (10 mins)
- Where Context comes from: static knowledge vs. dynamic data vs. conversation history (10 mins)
- Quick overview of vector databases, a light comparison of Qdrant vs. Pinecone — just enough, no deep dive (8 mins)
- **Build RAG by hand, without n8n**: use Postman/curl to call Voyage AI, turn Blazz's contracts/FAQs into vectors, and store them in Qdrant Cloud (27 mins)
- Hands-on: query the same API, turn a question into a vector, and get back the most relevant original text (15 mins)
- **Build the dynamic-data side**: set up Supabase, create a simple fake billing/account table, and load in the billing/plan fake data prepared in Unit 1 (15 mins)
- Wrap-up (5 mins)

## Deliverables

- A queryable Qdrant collection loaded with embeddings of Blazz's contracts/FAQs, verified via API to return the right passages
- A Supabase table loaded with fake billing data (the Unit 3 billing agent will query this)

## Homework

TBD

---

[← Previous: The Three Pillars of an Agent](unit-1.md) ｜ [Next: Multi-Agent Design & Building the Workflow →](unit-3.md)
