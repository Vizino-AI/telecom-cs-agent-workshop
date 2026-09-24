# Tools List

[← Back to course overview](README.md)

| Category | Tool | Purpose |
| --- | --- | --- |
| Automation platform | n8n Cloud | Core backend logic, workflow orchestration, Webhook/OAuth integration (account opened in Unit 3) |
| Language model | Gemini Flash | High-logic workflows, intent classification, RAG response generation |
| Language model | Gemini Pro | Collaborates with Gemini Flash, used for some task comparisons and fallback |
| Dev assistance | Claude Code | Natural-language tweaks, fake-data generation, keeps the no-code experience intact |
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
