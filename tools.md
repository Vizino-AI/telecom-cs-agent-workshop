# Tools Overview & Technical Decisions

[← Back to course overview](README.md)

In short, a vector database stores text after converting it into "semantic vectors" and searches by "semantic similarity." Blazz's contract clauses and FAQ content are first turned into a string of numbers (embeddings); when a user asks a question, it's converted into the same kind of number, and the database finds the closest-matching passages to hand back to the AI as reference — that's the core of RAG (Retrieval-Augmented Generation). The embedding API and Qdrant are two independent cloud services that know nothing about each other — as long as the vector dimensions match, they can be paired freely. [Unit 2](units/unit-2.md) calls both services' APIs directly to build the vector database, so the student understands the mechanism; [Unit 3](units/unit-3.md) then wires up the same calls using n8n's built-in nodes (or the HTTP Request node). Pinecone is another common option alongside Qdrant.

> 🔧 **Embedding provider: Voyage AI**. The project deliberately stays inside the Anthropic ecosystem as much as possible — Claude handles generation, Voyage AI handles embedding. Note that Claude (Anthropic) doesn't provide its own embedding API — **Voyage AI is Anthropic's officially recommended independent partner** (not an Anthropic product itself, but the official first choice), and it's called the same way: as an API — consistent with Unit 2's "call the raw API directly" approach. If n8n doesn't have a dedicated Voyage AI node, Unit 3 falls back to n8n's HTTP Request node, which works the same way.

> 🔧 **Why Supabase for dynamic data**: besides static knowledge (RAG), Context also includes mutable "dynamic data" like billing/account status, which is fundamentally something that lives in a database. Supabase is a managed cloud Postgres — its free tier is plenty for a teaching-scale project, and it follows the same cloud-first, don't-self-host principle as n8n Cloud and Qdrant Cloud. The account and table get set up in Unit 2; the billing agent queries it via an n8n node starting in Unit 3.

> 🔧 **Why n8n isn't the only path**: n8n (and even Voiceflow) could be replaced by newer tools later, and we don't want the student to come away thinking "you can only query data through n8n." Unit 2 first calls Voyage AI and Qdrant directly via Postman/curl, so the student understands RAG is fundamentally just two independent HTTP APIs; Unit 3 then shows that n8n's nodes are just a shell wrapping the same calls.

## Tool List

| Category | Tool | Purpose |
| --- | --- | --- |
| Automation platform | n8n Cloud | Core backend logic, workflow orchestration, Webhook/OAuth integration (account opened in Unit 3) |
| Language model | Claude 3.5 Sonnet | High-logic workflows, intent classification, RAG response generation |
| Language model | GPT-4o | Collaborates with Claude, used for some task comparisons and fallback |
| Dev assistance | Claude Code/Cursor | Natural-language tweaks, fake-data generation, keeps the no-code experience intact |
| API testing | Postman/curl | Unit 2 calls Voyage AI and Qdrant directly, hands-on with RAG's underlying mechanism |
| Embedding | Voyage AI | Turns text into vectors; Anthropic's officially recommended partner (Anthropic doesn't offer its own embedding API) |
| Conversational front end | Voiceflow | Designs the conversation flow, rolled out across web/WhatsApp/phone in stages |
| Vector database | Qdrant (or Pinecone) | Stores embeddings of Blazz's contracts and FAQs for RAG retrieval |
| Relational database | Supabase | Managed Postgres; stores dynamic data like billing/account status — table built in Unit 2, queried by the billing agent from Unit 3 |
| Team collaboration | Slack | Blazz's internal human-in-the-loop review |
| Email service | n8n Email/SMTP node | Automatically sends support forms and notifications |
| Local prep environment | Docker | Self-hosted n8n for practicing Advanced AI (LangChain) nodes |

## Prep Strategy

- Use a local Docker-hosted n8n instance to practice and hit rough edges ahead of time
- Get comfortable with how data flows through the Advanced AI (LangChain) nodes
- Combine full-stack experience with AI tooling to quickly stand up a test backend API
- Goal: be able to demonstrate real system-integration fluency when working through this with the student
