# Unit 4: Giving Blake a Knowledge Base — Vectors, Embeddings & RAG

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Explain the two core weaknesses of LLMs that RAG addresses: hallucination (an answer with no real grounding) and stale knowledge (frozen at training time)
- Explain why pasting a large reference document directly into a prompt doesn't scale — token count, and so cost and latency, grows with however much text is pasted in
- Explain how RAG fixes both: Retrieval finds the relevant excerpt from a vector database ahead of time, Augmentation appends it to the prompt so the model answers from it instead of guessing; adding new documents to that vector database keeps the model's effective knowledge current without retraining
- Explain what a vector database is and how similarity search works
- Describe the full RAG pipeline end to end (index → embed → store → search → augment) and recognize each step in a working n8n workflow

This unit is concepts plus an instructor walkthrough. The student does not build the RAG pipeline; in Unit 5 their agent searches the instructor's hosted RAG Search endpoint.

## Setup

None.

## Nice to Know

- **Hallucination**: an LLM's attention spreads thin over a long, generic context, so it fills gaps with plausible-sounding but ungrounded text
- **Stale knowledge**: an LLM only knows what existed up to its training cutoff — anything newer simply isn't in its weights
- **Why not just paste everything into the prompt**: it works for a handful of documents, but token count — and so cost and latency — scales with however much text gets pasted in
- **RAG's two halves**: Retrieval — search a vector database ahead of time for the most relevant chunks; Augmentation — append those chunks to the prompt so the model answers from them instead of guessing
- **Vector database**: stores each chunk as a vector (a list of numbers representing meaning) and finds the closest ones to a query vector by similarity search — Supabase's `vector` extension (pgvector) is what the instructor's demo uses
- **Index-time vs. query-time**: indexing (embed → store) happens once per document; search (embed the question → similarity search) happens on every customer message

## Class Content

- Review from last session, plan for today (5 mins)
- The two weaknesses of LLMs that RAG addresses: hallucination (attention spread thin, ungrounded answers) and stale knowledge (frozen at training time) (5 mins)
- Why pasting everything into the prompt doesn't scale: more reference text means more tokens, which means higher cost and slower responses (5 mins)
- How RAG solves both: Retrieval finds a precise excerpt from a vector database ahead of time, Augmentation appends it to the prompt so the model's attention is anchored to it; adding new documents to the vector database keeps the model's effective knowledge current (5 mins)
- What a vector database is and how similarity search works (10 mins)
- Instructor walkthrough (no student build): the 30-article Blazz knowledge base, how each article is embedded and stored, and the RAG Search workflow that embeds a question and returns the closest articles (30 mins)
- Live demo: ask the RAG Search endpoint questions in different wording (e.g. "orange light" when the articles say "amber") and compare with an answer given without RAG (20 mins)
- Wrap-up and Q&A (10 mins)

## Deliverables

No build deliverable. The student can explain the RAG pipeline in their own words and has seen it run against the 30-article Blazz knowledge base.

## Homework

Benchmark comparison: take the same 30-article knowledge base and test the same set of questions against three setups — (1) all 30 articles pasted directly into Scenario 2's system message, (2) all 30 articles concatenated into one Supabase Storage document (the Unit 3 pattern), (3) the instructor's hosted RAG Search endpoint. Score each answer with a summary/judge agent and compare quality, cost, and speed across the three.

---

[← Previous: Completing All Three Scenarios](unit-3.md) ｜ [Next: Building the Blazz Front Desk Agent →](unit-5.md)
