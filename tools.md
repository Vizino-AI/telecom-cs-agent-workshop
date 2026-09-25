# Tools Overview & Technical Decisions

[← Back to course overview](README.md)

## Tool List

| Category | Tool | Purpose |
| --- | --- | --- |
| Automation platform | self-hosted n8n | Core backend logic, workflow orchestration, Webhook/OAuth integration (account opened in Unit 2) |
| Dev assistance | Claude Code/Cursor | Natural-language tweaks, fake-data generation, keeps the no-code experience intact |
| API testing | Postman/curl | Unit 2 calls Supabase's REST API directly, hands-on with the underlying HTTP mechanism |
| Version control | Git + GitHub | Account and install done in Unit 1 |
| Code editor | Visual Studio Code | Installed in Unit 1 |
| Conversational front end | n8n Chat | Hosted Chat (n8n's own page) in Unit 2; switched to Embedded Chat, served from a custom HTML page, in Unit 4 |
| Relational database | Supabase | Managed Postgres; stores dynamic customer/billing data and chat memory — table built in Unit 2, queried by tools from Unit 2 onward |
| Object storage | Supabase Storage | Holds Scenario 2's FAQ and Scenario 3's contract terms as files, fetched via a Tool call — built in Unit 3, same Supabase project as the database |
| Team collaboration | Slack | Scenario 2's escalation tool (Unit 3), Blazz's internal human-in-the-loop review |
| Email service | n8n Email/SMTP node | Scenario 3's cancellation-form tool (Unit 3), and the confidence-fallback transcript email (Unit 4) |
| Local prep environment | Docker | Self-hosted n8n for practicing Advanced AI (LangChain) nodes |
