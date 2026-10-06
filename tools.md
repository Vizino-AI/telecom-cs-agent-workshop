# Tools Overview & Technical Decisions

[← Back to course overview](README.md)

## Tool List

| Category | Tool | Purpose |
| --- | --- | --- |
| Automation platform | self-hosted n8n | Core backend logic, workflow orchestration, Webhook/OAuth integration (account opened in Unit 2) |
| Dev assistance | Claude Code/Cursor | Natural-language tweaks, fake-data generation, keeps the no-code experience intact; in Unit 5 it acts as the MCP client for the n8n and Supabase MCP servers |
| API testing | Postman/curl | Unit 2 calls Supabase's REST API directly, hands-on with the underlying HTTP mechanism |
| Version control | Git + GitHub | Account and install done in Unit 1 |
| Code editor | Visual Studio Code | Installed in Unit 1 |
| Conversational front end | n8n Chat | Hosted Chat (n8n's own page), built in Unit 2 and used for the rest of the course |
| Relational database | Supabase | Managed Postgres; stores dynamic customer/billing data and chat memory — table built in Unit 2, queried by tools from Unit 2 onward |
| Object storage | Supabase Storage | Holds Scenario 3's contract terms, fetched via a Tool call (Unit 3); same Supabase project as the database |
| Vector database | Supabase Vector (pgvector) | Stores the Blazz knowledge base as embeddings, searched by the instructor's hosted RAG Search workflow — same Supabase project; walked through in Unit 4, called by the Front Desk Agent in Unit 5 |
| Embeddings | Gemini Embeddings API | Converts the Blazz knowledge base and incoming questions into vectors for RAG — shown in the Unit 4 walkthrough |
| Team collaboration | Slack | Scenario 2's escalation tool (Unit 3), Blazz's internal human-in-the-loop review |
| Email service | n8n Email/SMTP node | Scenario 1's Plan Change Request SOP and Scenario 3's cancellation-form tool (both Unit 3), and the Front Desk Agent's approval, follow-up and summary emails (Unit 5) |
| Local prep environment | Docker | Self-hosted n8n for practicing Advanced AI (LangChain) nodes |
