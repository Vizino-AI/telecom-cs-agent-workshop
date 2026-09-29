# Unit 3: Human-in-the-Loop & the Leap to Unstructured Data — Finishing Scenario 1, Starting Scenario 2

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Finish out Scenario 1's remaining Tools and its Plan Change Request SOP, reusing the Unit 2 pattern instead of starting from scratch
- Wire up human-in-the-loop escalation through two channels — Slack and Email — and use n8n Expressions to pull a field from an earlier node into that message instead of hardcoding it
- Distinguish structured data (tables) from unstructured data (documents, chat messages), and explain why unstructured data needs an LLM instead of a database query
- Apply the Unit 2 pattern to a new scenario by duplicating and adapting an existing workflow
- Store a reference document in Supabase Storage, and give an agent a Tool to fetch and read it

## Setup

Reuses the n8n instance, Supabase project, and LLM key from Unit 2 — including Supabase Storage, which lives in the same project. Two new accounts, needed from early in class (not just for the Scenario 2 build):

- **Slack**: a free workspace is enough; built during the human-in-the-loop segment, then reused for Scenario 2's escalation
- Email/SMTP: reuse an existing email account or n8n's built-in node; built during the human-in-the-loop segment for Scenario 1's Plan Change Request SOP

## Nice to Know

- **Reusing the Unit 2 pattern**: duplicate the Unit 2 workflow as a starting point for a new scenario — swap the system prompt and Tools, keep the Chat Trigger and Memory as they are
- **Supabase Storage basics**: buckets and files, and fetching a file's contents through a Tool call — the same "agent calls a Tool that hits Supabase" pattern as the database Tools, just for a document instead of a row
- **Slack Tool basics**: n8n's "Send and Wait for Response" node, with custom button labels (Confirm / Propose Other Time)
- **Email Tool basics**: sending an email from an n8n Tool node
- **n8n Expressions**: referencing another node's output field with `{{ $json.field }}` — what turns a hardcoded Email/Slack message into one that carries the actual customer, plan, or bill data through the workflow
- **Structured vs. unstructured data**: tables and rows vs. documents and free text, and why the latter needs an LLM to be usable at all — see [data-crash-course.md](../data-crash-course.md)

## Class Content

- Review from last session + questions (10 mins)
- Finish Scenario 1:
  - Build the `bills` and `travel_histories` tables and seed them (see [mock-data.md](../mock-data.md)) (10 mins)
  - Build two Tools querying them — bill lookup and travel-history lookup — reusing last session's pattern (10 mins)
  - Human-in-the-loop: build an Email Tool for the Plan Change Request SOP (submits to `planchanges@blazz.internal` — see [scenarios.md](../scenarios.md)) and a Slack Tool (Confirm / Propose Other Time buttons, to be reused for real in Scenario 2's escalation); along the way, introduce Variables & Expressions — pulling a field (customer name, the AI's summary of the request) from an earlier node into the message instead of hardcoding it (15 mins)
  - Wrap up: revisit Unit 2's Table 1 and fill in the Scenario 1 column as a review of everything built across both sessions (5 mins)
- Bridge: Scenario 1's data was all structured (tables); a lot of real-world data isn't — walk through the Data Crash Course (structured vs. unstructured, Supabase Database vs. Storage) (10 mins)
- Build Scenario 2 (Internet Outage Troubleshooting): duplicate the Unit 2 workflow, upload the troubleshooting FAQ to Supabase Storage, add a Tool that fetches it, add a Tool that checks `technician_availability` (demo customer: David Kim, Toronto, ON — matches technicians Priya Sharma and Marco Ricci; see [mock-data.md](../mock-data.md)), and wire in the Slack escalation Tool built earlier (Confirm / Propose Other Time) (30 mins)

## Deliverables

Two working n8n bots:

- Scenario 1 (billing), now complete with all Tools — identity verification, bill lookup, travel-history lookup — plus the Plan Change Request SOP wired to Email and Slack human-in-the-loop
- Scenario 2 (outage troubleshooting), with the FAQ in Supabase Storage, a fetch Tool, a technician-availability Tool, and the Slack escalation Tool (Confirm / Propose Other Time) reused from Scenario 1's build

## Homework

Build Scenario 3 (Cancellation & Retention) on your own: duplicate the workflow, upload the contract/termination-fee terms to Supabase Storage, add a Tool that fetches them, and reuse the Email Tool pattern for the cancellation form. Then fill in Unit 2's Table 1 — the Scenario 3 column — the same way you did for Scenario 1 in class.

---

[← Previous: Blazz's First Working Bot](unit-2.md) ｜ [Next: One Agent, Three Scenarios →](unit-4.md)
