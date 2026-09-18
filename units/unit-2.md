# Unit 2: Building Context

[← Back to course overview](../README.md)

## Learning Objectives

Understand Context's two faces — RAG for static knowledge, Supabase for dynamic data — and build both by calling raw APIs first, without n8n.

## Accounts to Set Up

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

- Review from last session, Q&A
- Where Context comes from: static knowledge vs. dynamic data vs. conversation history
- Quick overview of vector databases, a light comparison of Qdrant vs. Pinecone (just enough, no deep dive)
- **Build RAG by hand, without n8n**: use Postman/curl to call Voyage AI, turn Blazz's contracts/FAQs into vectors, and store them in Qdrant; then use the same API to run a query
- **Build the dynamic-data side**: set up Supabase, create a simple fake billing/account table (the "dynamic data" piece), and load in the billing/plan fake data prepared in Unit 1

### 90-Minute Rundown

| Time | Content |
| --- | --- |
| 0:00–0:10 | Review from last session, Q&A |
| 0:10–0:20 | Where Context comes from: static knowledge vs. dynamic data vs. conversation history |
| 0:20–0:28 | Quick vector-database overview, light comparison of Qdrant vs. Pinecone |
| 0:28–0:55 | Hands-on: call Voyage AI directly via Postman/curl, turn Blazz's contracts and FAQs into vectors, store them in Qdrant Cloud (no n8n) |
| 0:55–1:10 | Hands-on: query the same API, turn a question into a vector, and get back the most relevant original text |
| 1:10–1:25 | Hands-on: set up Supabase, create a simple fake billing/account table, load in dynamic data |
| 1:25–1:30 | Assign homework |

> **Why not just build this in n8n**: n8n's Embeddings/Vector Store nodes really are faster to pick up than calling raw APIs by hand — but the point is for the student to understand from day one that "this is really just two HTTP APIs," not just "drag nodes around in n8n to look things up." n8n is convenient, but it isn't the only way, and understanding stays intact even if it's swapped out later. Unit 3 immediately replaces this API pair with n8n nodes, so the student sees the node is just a shell around the same thing.

## Deliverables

- A queryable Qdrant collection loaded with embeddings of Blazz's contracts/FAQs, verified via API to return the right passages
- A Supabase table loaded with fake billing data (the Unit 3 billing agent will query this)

## Homework

_Not decided yet._

---

[← Previous: The Three Pillars of an Agent](unit-1.md) ｜ [Next: Multi-Agent Design & Building the Workflow →](unit-3.md)
