# Unit 4: Completing the Agent's Hands and Feet — End-to-End Tool Integration (Web Front End, Backend, Logging)

[← Back to course overview](../README.md)

## Learning Objectives

Wire the whole system into a working web-based customer-service experience a real person can use, with logging that makes it clear what the system is doing.

## Setup

- **Slack**: a free workspace is enough for the human-in-the-loop features used here
- Email/SMTP: reuse an existing email account or n8n's built-in node — usually no new signup needed

No new front-end tool or account needed — the chat interface is n8n's own Chat Trigger node, already available in the n8n instance set up in Unit 3.

## Nice to Know

- **Chat Trigger vs. a generic Webhook**: it speaks a built-in chat protocol (`sendMessage`/`loadPreviousSession`) and — with Hosted Chat mode — serves a ready-made chat UI directly, no separate front-end tool needed
- **Session continuity**: connecting a Memory node to the Chat Trigger (Load Previous Session → From Memory) is what lets the agent remember earlier turns in the same conversation
- **SMTP/email basics**: why you need to configure an outgoing mail server
- **The basics of logging**: who did what, and when

## Class Content

- Review from last session, Q&A (10 mins)
- Front end: swap Unit 3's generic Webhook trigger for n8n's **Chat Trigger** node, set Mode to Hosted Chat and make it public; wire a Memory node to both the trigger and the agent logic for conversation continuity; test end-to-end (15 mins)
- Backend: automatic support-form emails, Slack human-in-the-loop (Blazz's internal review) (25 mins)
- Logging: design a record of the conversation and the decisions made (who asked what, what the agent decided, whether it escalated to a human); wire the front end, backend, and logging into one complete end-to-end flow and test it (20 mins)
- Wrap-up (20 mins)

## Deliverables

A working end-to-end demo: a web-based conversation wired to the backend (email + Slack) with logging in place

## Homework

TBD

---

[← Previous: Building the Agent's Brains and Hands](unit-3.md) ｜ [Next: Hardening the Agent →](unit-5.md)
