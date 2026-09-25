# Unit 4: One Agent, Three Scenarios — Front-Desk Triage & Confidence Fallback

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Combine several independently-built agents into one workflow behind a single front-desk triage agent
- Design a triage agent that classifies an incoming request and hands off to the right specialist
- Have the Model report a confidence score, and treat "not confident" as its own outcome instead of forcing a guess
- Build a human fallback that emails a customer's verified identity and full conversation transcript to the call center
- Swap n8n's Hosted Chat for Embedded Chat, and serve it from a simple custom HTML page instead of n8n's own hosted page

## Setup

No new accounts — reuses everything from Units 2–3 (n8n, Supabase, LLM key, Slack, Email).

## Nice to Know

- **Multi-agent orchestration**: a front-desk/triage agent that classifies intent and hands off, versus sub-agents that do the specialized work
- **Confidence scoring**: asking the Model to report how sure it is, so "unsure" becomes a real branch in the workflow rather than a guess
- **Escalation via email**: an internal-facing email carrying identity + full transcript is a simple, reliable way to hand a live conversation to a human
- **Embedded Chat vs. Hosted Chat**: Hosted Chat serves n8n's own ready-made page; Embedded mode instead gives a small JS snippet to drop into your own HTML page
- **Just enough HTML**: a script tag and a bit of styling is all it takes to put the embedded chat on a page that looks like Blazz's, not n8n's

## Class Content

- Review from last session, Q&A (10 mins)
- Design and build the front-desk triage agent: classify the incoming message as Scenario 1 (billing), 2 (outage), 3 (cancellation), or unclear, and wire in the three scenario agents from Units 2–3 as its handoff targets inside one combined workflow (30 mins)
- Add a confidence score to each sub-agent's response; below a threshold, route to the fallback instead of replying directly (15 mins)
- Build the fallback: an Email Tool that sends the customer's verified identity and the full conversation transcript to the call center, then tells the customer a human will follow up (15 mins)
- Switch the front end from Hosted Chat to Embedded Chat: grab n8n's embed snippet and drop it into a simple custom HTML page with minimal Blazz branding (15 mins)
- Test all three scenarios plus an ambiguous, low-confidence case through the new embedded page; wrap-up (5 mins)

## Deliverables

A single n8n workflow, served through a simple custom HTML page (not n8n's own hosted page), that:

- Routes each incoming conversation to the right scenario agent via a front-desk triage agent
- Falls back to a human whenever confidence is low, by emailing the customer's identity and full transcript to the call center

## Homework

Write down 3–5 ambiguous or multi-intent customer messages that might confuse the triage agent (e.g. one that reads as both a billing question and a complaint). Bring them to test in Unit 5's stress test.

---

[← Previous: Completing All Three Scenarios](unit-3.md) ｜ [Next: Hardening the Agent →](unit-5.md)
