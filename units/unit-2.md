# Unit 2: Blazz's First Working Bot — Context, Memory & Tool Calling

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Distinguish static knowledge from dynamic data
- Plan an agentic workflow's system prompt, its three elements (Model/Context/Tool), and the environment it runs in
- Store data into a database, and query/filter it back out (e.g. look up one customer's record)
- Use Postman to verify data actually landed in the database correctly
- Work with core n8n mechanics: setting credentials, building nodes, and reading the input/output data flowing between them
- Explain how a chatbot holds a multi-turn conversation (Memory, the ReAct mechanism)
- Build a chatbot that calls the right tool at the right time, guided by a clear, specific description on each tool, and follows system instructions to complete a task

## Setup

- **n8n Cloud**: account needed for this unit's node-building
- **Supabase**: free tier; stores Scenario 1's fake billing/customer data and, via its Postgres database, the bot's chat memory
- **Postman**: to verify the data inserted via SQL actually landed correctly, before n8n starts reading it
- **LLM API key**: for the AI Agent node (Gemini Flash or GPT-4o)

## Nice to Know

- **What a system prompt is**: how instructions shape an LLM agent's behavior
- **HTTP basics**: request/response, methods (GET/POST), endpoints, headers, body
- **Basic relational-database concepts**: tables, columns, rows
- **Querying/filtering data**: looking up a specific row by a key column (e.g. `WHERE phone_number = ...`) — what identity verification and the lookup tools all depend on
- **The ReAct pattern**: how an agent alternates between reasoning and acting (Thought → Action → Observation) to hold a multi-turn conversation and call tools

## Class Content

- Plan the agentic workflow: draft the system prompt, walk through the three elements (Model/Context/Tool), and map out the environment it runs in, using Table 1. Fill in only the Scenario 1 column now — Scenario 2 and 3 are homework (10 mins)
- Review Scenario 1's fake data, then use Claude to write the SQL that creates the table(s) and inserts the data (30 mins)
- Open a Postman account and use it to query Supabase directly, confirming the data just inserted via SQL actually landed correctly — this is the checkpoint that lets us trust the data n8n reads later (10 mins)
- Build n8n's Chat Trigger node and enable CORS (10 mins)
- Build the AI Agent node, connect it to the LLM, and add a **Chat Memory** node — wire it to **both** the Chat Trigger and the AI Agent (connecting it only to the Chat Trigger is a common mistake that leaves the AI Agent itself with no memory). Confirm the chatbot holds a multi-turn conversation (10 mins)
- Build three Tool nodes for the AI Agent, each querying Supabase and each given a clear, specific description — the agent reads these descriptions to judge which tool fits the moment, so imprecise wording here means wrong or missed tool calls later:
  1. Identity verification (15 mins)
  2. Bill lookup (10 mins)
  3. Rate-plan lookup (10 mins)

## Deliverables

A working n8n chatbot for Scenario 1 (billing inquiry & upsell) that:

- Holds a multi-turn conversation via the Chat Trigger node and Postgres-backed chat memory
- Verifies the customer's identity, looks up their bill, and looks up their rate plan — each through its own Tool call, with the agent picking the right one based on what's being asked
- Runs on Scenario 1's fake data, stored in Supabase

## Homework

Review Scenario 1 with the bot you built in class:

- Test it in your own words, not the demo script, and confirm the agent picks the right tool — identity verification, bill lookup, or rate-plan lookup — for each request
- Try to get it to reveal billing or plan details before identity is verified; if it does, that's a gap worth bringing to next class
- Note down anything that broke or felt fragile

Fill in the Scenario 2 and Scenario 3 columns of Table 1 (System Prompt, Model, Context, Tool, Environment) — planning only, no build yet. Scenario 2's actual bot waits until Unit 3, once RAG is covered.

## Table 1

| | Scenario 1 | Scenario 2 | Scenario 3 |
| --- | --- | --- | --- |
| **System Prompt** | | | |
| **Model** | | | |
| **Context** | | | |
| **Tool** | | | |
| **Environment** | | | |

---

[← Previous: The Three Pillars of an Agent](unit-1.md) ｜ [Next: Building the Agent's Brains and Hands →](unit-3.md)
