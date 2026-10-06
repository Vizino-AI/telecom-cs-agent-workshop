# Unit 5: Building the Blazz Front Desk Agent — MCP, Tools & Human-in-the-Loop

[← Back to course overview](../README.md)

## Learning Objectives

By the end of this unit, the student can:

- Explain what MCP (Model Context Protocol) is, and use Claude Code as an MCP client to work with n8n and Supabase
- Build one front-desk agent, Blazz Front Desk Agent, that handles all three scenarios by giving it as many tools as it needs
- Add three human-in-the-loop patterns: real-time approval, human follow-up, and an internal summary email
- Use Claude Code to read the Supabase data and design three end-to-end "ultimate test" scenarios, run them, and judge the result
- Discuss what makes a good AI customer service agent

## Setup

- Download and install [Claude Code](https://claude.com/claude-code) (the MCP client)
- Connect the n8n MCP server and the Supabase MCP server to Claude Code through Connectors
- The instructor shares the URL and API key for the hosted RAG Search endpoint, so the student's agent can search the Blazz knowledge base without building RAG on their own n8n
- Everything else is reused from Units 2–4 (n8n, Supabase, Gemini key, Gmail/Slack)

## Nice to Know

- **MCP (Model Context Protocol)**: a standard way for an AI app to connect to outside tools and data, so any MCP client can use any MCP server
- **MCP client vs. MCP server**: Claude Code is the client; n8n and Supabase each expose a server that the client talks to
- **One agent, many tools**: instead of one agent per scenario, a single agent with a well-described tool for each job. The tool descriptions are what the Model reads to decide which one to call
- **Real-time approval**: the workflow pauses at a high-risk step and waits for a human to approve or decline before the agent can promise anything
- **Human follow-up**: the agent pauses, asks a human for the answer it does not have, and relays only what the human actually wrote
- **Summary email**: an internal-only record of each finished conversation

## Class Content

- Review from last session, Q&A (5 mins)
- Install the n8n MCP server (20 mins)
  - Download Claude Code (the MCP client)
  - Use Connectors to connect the n8n and Supabase MCP servers
- Build the Blazz Front Desk Agent: add as many tools as needed, including RAG Search, called over the instructor's hosted endpoint with an HTTP Request tool (15 mins)
- Add human-in-the-loop (25 mins)
  - Real-time approval
  - Follow-up
  - Summary
- Three ultimate test scenarios (15 mins): ask Claude Code to read the data in Supabase through the Supabase MCP server and come up with three ultimate test scenarios for the agent, then run them against the Front Desk Agent
- Open discussion: what makes a good AI customer service agent? (10 mins)

## Deliverables

A single Blazz Front Desk Agent workflow in n8n that:

- Handles all three scenarios through one set of tools
- Asks a human for real-time approval before any high-risk commitment
- Asks a human for follow-up when it cannot answer, and relays the reply faithfully
- Sends an internal summary email when a conversation ends
- Has been run through three ultimate test scenarios that Claude Code designed from the Supabase data

## Homework

How would you evaluate the performance of a customer service chatbot? Write down your answer.

---

[← Previous: Giving Blake a Knowledge Base](unit-4.md) ｜ [Back to course overview](../README.md)
