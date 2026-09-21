# Tools Overview & Technical Decisions

[← Back to course overview](README.md)

In short, a vector database stores text after converting it into "semantic vectors" and searches by "semantic similarity." Blazz's contract clauses and FAQ content are first turned into a string of numbers (embeddings); when a user asks a question, it's converted into the same kind of number, and the database finds the closest-matching passages to hand back to the AI as reference — that's the core of RAG (Retrieval-Augmented Generation). The embedding API and Qdrant are two independent cloud services that know nothing about each other — as long as the vector dimensions match, they can be paired freely. [Unit 3](units/unit-3.md) builds the vector database directly with n8n's built-in Embeddings/Vector Store nodes (or the HTTP Request node, if a dedicated node isn't available) — by then the student has already called a similar raw REST API by hand for Supabase in Unit 2, so the node isn't a mysterious black box. Pinecone is another common option alongside Qdrant.

> 🔧 **Embedding provider: Voyage AI**. The generation model and the embedding model don't need to share a vendor — as already noted above, the embedding API and Qdrant are independent services that just need matching vector dimensions to pair freely, and the same logic applies to picking an embedding provider independent of which LLM (Gemini Flash) handles generation. Voyage AI stands on its own merits here as a strong, retrieval-tuned embedding model, and — like Supabase in Unit 2 — it's called directly as a raw API, consistent with the "call the raw API first" principle the student already practices. If n8n doesn't have a dedicated Voyage AI node, Unit 3 falls back to n8n's HTTP Request node, which works the same way.

> 🔧 **Why Supabase for dynamic data**: besides static knowledge (RAG), Context also includes mutable "dynamic data" like billing/account status, which is fundamentally something that lives in a database. Supabase is a managed cloud Postgres — its free tier is plenty for a teaching-scale project, and it follows the same cloud-first, don't-self-host principle as n8n Cloud and Qdrant Cloud. The account and table get set up in Unit 2; the billing agent queries it via an n8n node starting in Unit 3.

> 🔧 **Why n8n isn't the only path**: n8n could be replaced by newer tools later, and we don't want the student to come away thinking "you can only query data through n8n." Unit 2 first calls Supabase's REST API directly via Postman/curl, so the student understands a backend lookup is fundamentally just an HTTP API; Unit 3 then shows that n8n's Supabase node — and its RAG-building nodes — are just a shell wrapping the same kind of calls.

> 🔧 **Why n8n's own Chat Trigger instead of Voiceflow**: n8n's Chat Trigger node ships a working chat UI (Hosted Chat mode) for free — no separate front-end tool, account, or embed setup needed. The trade-off is real: it's web-only, with none of Voiceflow's visual conversation-flow design or multi-channel (phone/WhatsApp) deployment. Given the course's time budget, one fewer tool to learn and a front end that "just works" wins out — see [Unit 4](units/unit-4.md).

## Tool List

| Category | Tool | Purpose |
| --- | --- | --- |
| Automation platform | n8n Cloud | Core backend logic, workflow orchestration, Webhook/OAuth integration (account opened in Unit 3) |
| Language model | Gemini Flash | High-logic workflows, intent classification, RAG response generation |
| Language model | GPT-4o | Collaborates with Gemini Flash, used for some task comparisons and fallback |
| Dev assistance | Claude Code/Cursor | Natural-language tweaks, fake-data generation, keeps the no-code experience intact |
| API testing | Postman/curl | Unit 2 calls Supabase's REST API directly, hands-on with the underlying HTTP mechanism |
| Version control | Git + GitHub | Account and install done in Unit 1 |
| Code editor | Visual Studio Code | Installed in Unit 1 |
| Embedding | Voyage AI | Turns text into vectors; strong retrieval-tuned embedding model, called as a raw API independent of the generation LLM |
| Conversational front end | n8n Hosted Chat | Built-in chat UI served directly by the Chat Trigger node — web only, no separate tool or account needed |
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
