# Unit 4: Giving Blake a Knowledge Base — Vectors, Embeddings & RAG

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Explain the two core weaknesses of LLMs that RAG addresses: hallucination (an answer with no real grounding) and stale knowledge (frozen at training time)
- Explain why pasting a large reference document directly into a prompt doesn't scale — token count, and so cost and latency, grows with however much text is pasted in
- Explain how RAG fixes both: Retrieval finds the relevant excerpt from a vector database ahead of time, Augmentation appends it to the prompt so the model answers from it instead of guessing; adding new documents to that vector database keeps the model's effective knowledge current without retraining
- Explain what a vector database is and how similarity search works
- Build a full RAG pipeline end to end: upload a document set to Supabase Storage, index it into a Supabase vector table via the Gemini Embeddings API, and rewire an existing agent to search it through a dedicated RAG Search sub-workflow

## Setup

Reuses the n8n instance, Supabase project (including the Storage bucket from Unit 3), and Gemini API key from earlier units — if it hasn't already been created, get one free from [Google AI Studio](https://aistudio.google.com/apikey). No new accounts beyond that — enable the `vector` extension in Supabase and create the `kb_chunks` table (see [mock-data.md](../mock-data.md)).

## Nice to Know

- **Hallucination**: an LLM's attention spreads thin over a long, generic context, so it fills gaps with plausible-sounding but ungrounded text
- **Stale knowledge**: an LLM only knows what existed up to its training cutoff — anything newer simply isn't in its weights
- **Why not just paste everything into the prompt**: it works for a handful of documents, but token count — and so cost and latency — scales with however much text gets pasted in
- **RAG's two halves**: Retrieval — search a vector database ahead of time for the most relevant chunks; Augmentation — append those chunks to the prompt so the model answers from them instead of guessing
- **Vector database**: stores each chunk as a vector (a list of numbers representing meaning) and finds the closest ones to a query vector by similarity search — Supabase's `vector` extension (pgvector) is what we use
- **Index-time vs. query-time**: indexing (chunk → embed → store) happens once per document; search (embed the question → similarity search) happens on every customer message
- **Discovering model names via the API**: rather than guessing or hardcoding a model string, call the provider's List Models endpoint to see what's actually available and what each one supports (e.g. `embedContent`) — worth doing any time a new model type, like embeddings, gets used for the first time

## Class Content

- Review from last session, plan for today (5 mins)
- The two weaknesses of LLMs that RAG addresses: hallucination (attention spread thin, ungrounded answers) and stale knowledge (frozen at training time) (5 mins)
- Why pasting everything into the prompt doesn't scale: more reference text means more tokens, which means higher cost and slower responses (5 mins)
- How RAG solves both: Retrieval finds a precise excerpt from a vector database ahead of time, Augmentation appends it to the prompt so the model's attention is anchored to it; adding new documents to the vector database keeps the model's effective knowledge current (5 mins)
- Explain what a vector database is and how similarity search works (10 mins)
- Build: turn Scenario 2's FAQ-troubleshooting agent into a full knowledge-base bot —
  - Review the prepared data: the 30-article Blazz knowledge base (5 mins)
  - Upload the 30 articles to Supabase Storage and create the `kb_chunks` table (10 mins)
  - Get a Gemini API key from Google AI Studio (reuse the one from Unit 2 if already created), then call the List Models endpoint with it to find the embedding model's exact name (5 mins)
  - Build the RAG indexing workflow: call the Gemini Embeddings API with that model name to convert each article into a vector and store it in `kb_chunks` (20 mins)
  - Test the indexing result: mock a customer question and call the Embeddings API to confirm it converts correctly (10 mins)
  - Build the RAG Search sub-workflow: embed the incoming question, query `kb_chunks` for the closest matches, and return them (20 mins)
  - Rewire Scenario 2's agent to call the RAG Search sub-workflow instead of its single-document FAQ fetch (15 mins)

> Heads up: this totals ~115 minutes against a 90-minute slot — the tightest unit yet. The indexing workflow and the RAG Search sub-workflow are the most compressible steps; have a partially-built template ready for either in case time runs short, the same fallback approach as Unit 3's Scenario 3 build.

## Deliverables

Scenario 2's agent upgraded from a single-document FAQ fetch to a full RAG pipeline: the 30-article Blazz knowledge base uploaded to Supabase Storage, indexed into a Supabase vector table (`kb_chunks`) via the Gemini Embeddings API, and searched through a RAG Search sub-workflow the agent calls on every question.

## Homework

Benchmark comparison: take the same 30-article knowledge base and test the same set of questions against three setups — (1) all 30 articles pasted directly into Scenario 2's system message, (2) all 30 articles concatenated into one Supabase Storage document (the Unit 3 pattern), (3) today's RAG pipeline. Score each answer with a summary/judge agent and compare quality, cost, and speed across the three.

---

[← Previous: Completing All Three Scenarios](unit-3.md) ｜ [Next: One Agent, Three Scenarios →](unit-5.md)
