# Unit 1: The Three Pillars of an Agent — Context, Tool, Model

[← Back to course overview](../README.md)

## Learning Objectives

Build the mental model "Agent = Model + Tool + Context," and learn to judge, for a given customer-service scenario, which information belongs in which pillar.

## Before Class

- Read: [Modern Agent = LLM + Context + Tools](https://github.com/bojieli/ai-agent-book/blob/main/book-en/chapter1.md#modern-agent--llm--context--tools)
- List a few examples of what company data an AI customer-service agent would need to do its job — e.g. FAQ, phone plans, customer data, you name it. Just examples; strategy and methods for preparing this data get discussed in class.

## Setup

GitHub account, Visual Studio Code, Git.

## Nice to Know

- **What an API is**: the interface for talking to an external system, and why a Tool needs one
- **The idea of a no-code automation platform**: why use n8n instead of writing code

## Class Content

- Intro: project goals, the three-pillar framework, the five-unit roadmap (10 mins)
- Discuss the pre-class list of company data types (FAQ, phone plans, customer data, etc.): strategies and methods for actually preparing/gathering each kind (15 mins)
- Break down Model/Tool/Context using the Blazz scenario — Model is mainly about division of labor (Claude for high-logic work, GPT-4o collaborates), plus which decisions go to the Model vs. which are hard-coded in nodes (15 mins)
- Review the [three core scenarios](../scenarios.md) together: check whether the example data prepared so far is complete enough for each, sort into Context vs. Tool (20 mins)
- Fill in any gaps found in that review — prepare the remaining example data points for Blazz (plan pricing, contract terms, FAQs) (15 mins)
- Sketch a first-draft agent architecture diagram, framing out the three Model/Tool/Context blocks (15 mins)

## Deliverables

- A first-draft agent architecture diagram (Model/Tool/Context)
- Example data for Blazz, checked against the three core scenarios and tagged as Context or Tool

## Homework

Clean up and organize the company data prepared in class into a usable format — it gets imported into the "Context" in Unit 2.

---

[Next: Building Context →](unit-2.md)
