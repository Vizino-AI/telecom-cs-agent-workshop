# Unit 2: Blazz's First Working Bot — Context, Memory & Tool Calling

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Distinguish static knowledge from dynamic data
- Plan an agentic workflow's system prompt, its three elements (Model/Context/Tool), and the environment it runs in
- Store data into a database, query/filter it back out, and confirm it landed correctly using Supabase's own dashboard
- Work with core n8n mechanics: setting credentials, building nodes, and reading the input/output data flowing between them
- Explain how a chatbot holds a multi-turn conversation (Memory, the ReAct mechanism)
- Build a chatbot that calls the right tool at the right time, guided by a clear, specific description on each tool, and follows system instructions to complete a task

## Setup

- **n8n Cloud**: account needed for this unit's node-building
- **Supabase**: free tier; stores Scenario 1's fake billing/customer data and, via its Postgres database, the bot's chat memory
- **LLM API key**: for the AI Agent node

## Nice to Know

- **What a system prompt is**: how instructions shape an LLM agent's behavior
- **Basic relational-database concepts**: tables, columns, rows
- **Querying/filtering data**: looking up a specific row by a key column (e.g. `WHERE phone_number = ...`) — what identity verification depends on
- **The ReAct pattern**: how an agent alternates between reasoning and acting (Thought → Action → Observation) to hold a multi-turn conversation and call tools

## Class Content

- Plan the agentic workflow: draft the system prompt, walk through the three elements (Model/Context/Tool), and map out the environment it runs in, using Table 1's Scenario 1 column (10 mins)
- Review Scenario 1's fake data, then use Claude to write the SQL that creates the table(s) and inserts the data; confirm the rows landed correctly in Supabase's own Table Editor — no separate tool needed (30 mins)
- Build n8n's Chat Trigger node and enable CORS (10 mins)
- Build the AI Agent node, connect it to the LLM, and add a **Chat Memory** node — wire it to **both** the Chat Trigger and the AI Agent. Confirm the chatbot holds a multi-turn conversation (10 mins)
- Build one Tool node for the AI Agent — identity verification — querying Supabase, with a clear, specific description so the agent knows when to call it (15 mins)

## Deliverables

A working n8n chatbot for Scenario 1 (billing inquiry & upsell) that:

- Holds a multi-turn conversation via the Chat Trigger node and Postgres-backed chat memory
- Verifies the customer's identity through a Tool call
- Runs on Scenario 1's fake data, stored in Supabase

## Homework

Review what you built today and try to rebuild it from scratch on your own — Chat Trigger, AI Agent, Chat Memory, and the identity-verification Tool.

## Table 1

| | Scenario 1 | Scenario 2 | Scenario 3 |
| --- | --- | --- | --- |
| **System Prompt** | | | |
| **Model** | | | |
| **Context** | | | |
| **Tool** | | | |
| **Environment** | | | |

---

[← Previous: The Three Pillars of an Agent](unit-1.md) ｜ [Next: Completing All Three Scenarios →](unit-3.md)
