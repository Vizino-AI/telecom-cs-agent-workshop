# Unit 4: End-to-End Integration (Web Front End, Backend, Logging)

[← Back to course overview](../README.md)

## Learning Objectives

Wire the whole system into a working web-based customer-service experience a real person can use, with logging that makes it clear what the system is doing.

## Setup

- **Voiceflow**: has a free tier (limited features/usage, enough for this course); going live or scaling up may require a paid plan
- **Slack**: a free workspace is enough for the human-in-the-loop features used here
- Email/SMTP: reuse an existing email account or n8n's built-in node — usually no new signup needed
- (Needed for homework) **Twilio**: required for WhatsApp/phone integration; has a free trial allowance, but a real phone number/production message volume requires a paid plan plus usage-based billing

## Nice to Know

- **Webhooks (two-way)**: the Voiceflow front end calls the n8n backend, which replies back to the front end
- **SMTP/email basics**: why you need to configure an outgoing mail server
- **The basics of logging**: who did what, and when

## Class Content

- Review from last session, Q&A (10 mins)
- Front end: design the conversation UI in Voiceflow, **first version covers only the "web" channel (web widget)** — get the full flow working end-to-end before expanding to other channels (25 mins)
- Backend: automatic support-form emails, Slack human-in-the-loop (Blazz's internal review) (25 mins)
- Logging: design a record of the conversation and the decisions made (who asked what, what the agent decided, whether it escalated to a human); wire the web front end, backend, and logging into one complete end-to-end flow and test it (20 mins)
- Wrap-up (10 mins)

## Deliverables

A working end-to-end demo: a web-based conversation wired to the backend (email + Slack) with logging in place

## Homework

TBD

---

[← Previous: Multi-Agent Design & Building the Workflow](unit-3.md) ｜ [Next: Hardening →](unit-5.md)
