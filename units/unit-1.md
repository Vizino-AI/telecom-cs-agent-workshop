# Unit 1: The Three Pillars of an Agent — Context, Tool, Model

[← Back to course overview](../README.md)

## Learning Objectives

Build the mental model "Agent = Model + Tool + Context," and learn to judge, for a given customer-service scenario, which information belongs in which pillar.

## Pre-Reading

[Modern Agent = LLM + Context + Tools](https://github.com/bojieli/ai-agent-book/blob/main/book-en/chapter1.md#modern-agent--llm--context--tools)


## Setup

Done live in class: GitHub account, Visual Studio Code, Git.

## Background Knowledge Needed

- **What an API is**: the interface for talking to an external system, and why a Tool needs one
- **The idea of a no-code automation platform**: why use n8n instead of writing code

## Class Content

- Intro: project goals, the three-pillar framework, the five-unit roadmap (15 mins)
- Break down Model/Tool/Context using the Blazz scenario — Model is mainly about division of labor (Claude for high-logic work, GPT-4o collaborates), plus which decisions go to the Model vs. which are hard-coded in nodes (15 mins)
- Review the [three core scenarios](../scenarios.md) together: for each, discuss what a customer-service person (or agent) needs to know — company data, customer info, background knowledge — sort into Context vs. Tool, and check whether the fake data prepared so far is complete enough to support all three (25 mins)
- Fill in any gaps found in that review — prepare the remaining example data points for Blazz (plan pricing, contract terms, FAQs) (15 mins)
- Sketch a first-draft agent architecture diagram, framing out the three Model/Tool/Context blocks (20 mins)

## Deliverables

- A first-draft agent architecture diagram (Model/Tool/Context)
- Example data for Blazz, checked against the three core scenarios and tagged as Context or Tool

## Homework

TBD

---

[Next: Building Context →](unit-2.md)
