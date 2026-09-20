# Unit 1: The Three Pillars of an Agent — Model, Context, Tool

[← Back to course overview](../README.md)

## Learning Objectives

Build the mental model "Agent = Model (brain) + Context (eyes) + Tool (hands & feet)," and learn to judge, for a given customer-service scenario, which information or decision belongs in which pillar.

## Before Class

- Read: [Modern Agent = LLM + Context + Tools](https://github.com/bojieli/ai-agent-book/blob/main/book-en/chapter1.md#modern-agent--llm--context--tools)
- List a few examples of what company data an AI customer-service agent would need to do its job — e.g. FAQ, phone plans, customer data, you name it. Just examples; strategy and methods for preparing this data get discussed in class.

## Setup

GitHub account, Visual Studio Code, Git.

## Nice to Know

- **What an API is**: the interface for talking to an external system, and why a Tool needs one
- **The idea of a no-code automation platform**: why use n8n instead of writing code

## Class Content

### 1. Intro: the formula, the roadmap (10 mins)

- Open with the formula: **Agent = Model + Context + Tool** — and the analogy that makes it stick: Model is the brain, Context is the eyes, Tool is the hands & feet.
- Immediately map the formula onto the five units, so the student sees this workshop as "build one body part per unit, then wire them together into one working agent":
  - **Context (eyes)** → Unit 2 — static knowledge via RAG, dynamic customer data via Supabase
  - **Model + Tool (brains + hands)** → Unit 3 — multi-agent workflow, each sub-agent given its own Context and Tool
  - **Tool (hands & feet), completed** → Unit 4 — the web front end, Slack handoff, email
  - **All three, hardened** → Unit 5 — guardrails and reliability
- Preview the deliverable: a working multi-agent customer-service system for Blazz.

### 2. Discuss the pre-class company data list (15 mins)

- Walk through the student's pre-class list of company data types (FAQ, phone plans, customer data, etc.)
- For each item, discuss where it would actually come from at a real telecom company (CRM export, billing system, support wiki) and how to get it into a usable format
- Don't sort into Context vs. Tool yet — that happens in the scenario review below, once the student has seen all three pillars broken down

### 3. Break down Model / Context / Tool using one Blazz scenario (15 mins)

Run a single running example — Scenario 1's "Why did my bill jump to over $2,000 this month?" — through all three pillars, so the student sees them acting on the same question instead of as three abstract definitions:

- **Model (brain)**: what judgment calls does it make here? Billing or technical? Proactively upsell or not? How to phrase the explanation? Introduce model division of labor — Claude for higher-logic reasoning and negotiation (e.g. the retention conversation in Scenario 3), GPT-4o for lighter classification or draft generation.
- Draw the line between a **Model decision** and a **hard-coded rule**: "if confidence < 0.7, escalate to Slack" is not the Model deciding — it's a fixed rule sitting in an n8n node. This line is exactly what Unit 3's workflow design will operationalize.
- **Context (eyes)**: what does the Model need to see to answer this? The customer's usage data (dynamic → Supabase), the rate-plan rules (static → RAG), and business rules embedded in the system prompt — e.g. Scenario 3's "explain the termination fee before offering the retention deal" is a Context rule, not something the Model improvises.
- **Tool (hands & feet)**: what actions can it take? Query Supabase for the bill detail, notify Slack, send an email. Rule of thumb: anything that changes external state or needs precise, real-time data must be a Tool call — never let the Model "recall" a number from memory.

### 4. Review the three core scenarios together (20 mins)

- Walk through [scenarios.md](../scenarios.md) as a group
- For each scenario, fill in a 3-column worksheet together, live:

  | Scenario | Context | Tool | Model judgment |
  | --- | --- | --- | --- |
  | Billing inquiry & upsell | Customer usage data, rate-plan sheet | Supabase billing API | Diagnose the roaming charge; decide whether to upsell |
  | Outage troubleshooting | Troubleshooting FAQ (RAG) | Slack notification to a technician | Judge whether the software fix failed → escalate |
  | Cancellation & retention | Contract terms (termination fee), retention-offer rules | Email node (cancellation form) | Read sentiment; decide whether to offer the retention deal first |

- Cross-check this against the example data the student prepared before class: is there enough raw material for each scenario? Flag any gaps for step 5.

### 5. Fill remaining data gaps (15 mins)

- Prepare whatever example data step 4 turned up as missing (plan pricing, contract terms, FAQs)

### 6. Sketch a first-draft architecture diagram (15 mins)

- Draw three boxes — Model / Context / Tool — and sketch how [architecture.md](../architecture.md)'s flow (triage → route → look up or act → check confidence → reply or escalate) moves between them
- Tie this to the "Thought → Action → Observation" loop: the Model thinks (Thought), calls a Tool (Action), the result updates Context (Observation), and the loop repeats until the agent replies or escalates
- This diagram is today's main deliverable — it doesn't need to be polished, just correct

## Deliverables

- A first-draft agent architecture diagram (Model/Context/Tool, with the Thought → Action → Observation loop sketched between them)
- Example data for Blazz, checked against the three core scenarios and tagged as Context, Tool, or a Model judgment call

## Homework

Clean up and organize the company data prepared in class into a usable format — it gets imported into the "Context" in Unit 2.

---

[Next: Building the Agent's Eyes →](unit-2.md)
