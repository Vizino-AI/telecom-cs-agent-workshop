# Unit 3: Completing All Three Scenarios — Tool Wiring & Human-in-the-Loop

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Finish out a scenario's remaining Tools, reusing an established pattern instead of starting from scratch each time
- Apply the Unit 2 pattern (Chat Trigger + AI Agent + Memory + Tools) to a new scenario, by duplicating and adapting an existing workflow
- Store a reference document in Supabase Storage, and give an agent a Tool to fetch and read it
- Wire up human-in-the-loop escalation through two different channels: Slack and Email

## Setup

Reuses the n8n instance, Supabase project, and LLM key from Unit 2 — including Supabase Storage, which lives in the same project. Two new accounts:

- **Slack**: a free workspace is enough; for Scenario 2's escalation tool
- Email/SMTP: reuse an existing email account or n8n's built-in node; for Scenario 3's cancellation-form tool

## Nice to Know

- **Reusing the Unit 2 pattern**: duplicate the Unit 2 workflow as a starting point for a new scenario — swap the system prompt and Tools, keep the Chat Trigger and Memory as they are
- **Supabase Storage basics**: buckets and files, and fetching a file's contents through a Tool call — the same "agent calls a Tool that hits Supabase" pattern as the database Tools, just for a document instead of a row
- **Slack Tool basics**: posting a message to a channel from an n8n Tool node
- **Email Tool basics**: sending an email from an n8n Tool node

## Class Content

- Review from last session: what's built (Scenario 1's Chat Trigger, AI Agent, Memory, identity-verification Tool) and today's plan (10 mins)
- Finish Scenario 1: build the bill-lookup and rate-plan-lookup Tools, reusing last time's pattern (20 mins)
- Build Scenario 2 (Internet Outage Troubleshooting): duplicate the Unit 2 workflow, upload the troubleshooting FAQ to Supabase Storage, add a Tool that fetches it, and add a Slack Tool that escalates to a human supervisor when the fix fails (30 mins)
- Build Scenario 3 (Cancellation & Retention): duplicate the workflow again, upload the contract/termination-fee terms to Supabase Storage, add a Tool that fetches them, and add an Email Tool that sends the cancellation form (30 mins)

> Heads up: this is already a full 90 minutes with zero buffer, and Unit 2 ran long even with a lighter plan. The two full-scenario builds are the likely overflow points — duplicating the Unit 2 workflow instead of rebuilding from scratch is the main time-saver already baked in here, but have a fallback ready to demo Scenario 3's build rather than have everyone build it hands-on if time is short.

## Deliverables

Three working n8n bots:

- Scenario 1 (billing), now complete with all three Tools: identity verification, bill lookup, rate-plan lookup
- Scenario 2 (outage troubleshooting), with the FAQ in Supabase Storage, a fetch Tool, and a Slack escalation Tool
- Scenario 3 (cancellation & retention), with contract terms in Supabase Storage, a fetch Tool, and an Email Tool for the cancellation form

## Homework

Test Scenario 2 and Scenario 3 the same way you tested Scenario 1: use your own words, try to break them (e.g. ask about an outage issue that's not in the FAQ, or try to skip past the retention offer), and note down anything that felt fragile.

---

[← Previous: Blazz's First Working Bot](unit-2.md) ｜ [Next: One Agent, Three Scenarios →](unit-4.md)
