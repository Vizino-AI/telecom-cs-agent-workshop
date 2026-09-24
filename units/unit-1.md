# Unit 1: The Three Components of an Agent — Model, Context, Tool

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

## Topics Covered

- Course goals and a preview of the end-to-end system, with a live high-level architecture sketch
- The agent's three elements — Model, Context, Tool — and how they map to the rest of the course
- A quick survey of common agent types (search, file-reading, coding, ...)
- A deep dive into Blazz's customer-service scenarios: common problems, SOPs, the data each needs, and how to delegate the SOP to an agent
- Mapping each step of that SOP onto Model / Context / Tool

## Deliverables

- A first-draft workflow for handling Blazz's most common customer-service SOP, mapped onto Model / Context / Tool
- Example company data, checked against what that SOP needs

## Homework

1. Refine the workflow sketched in class
2. Clean up and organize the company data gathered: dynamic data (billing/plan) gets imported into Supabase in Unit 2, and static knowledge (FAQ/contracts) becomes the RAG knowledge base in Unit 3

---

[Next: Blazz's First Working Bot →](unit-2.md)
