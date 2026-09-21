# Unit 2: Building the Agent's Eyes — Context

[← Back to course overview](../README.md)

## Learning Objectives

Understand Context's three shapes — static text small enough to paste directly into a system prompt, structured dynamic data (Supabase tables), and dynamic files (Supabase Storage) — and get hands-on with the table and file halves by calling Supabase's REST API directly, without n8n. Large-scale static knowledge (RAG) is covered conceptually this unit and gets built next unit using n8n's built-in nodes.

## Setup

- **Supabase**: free tier (plenty for this course's scale, includes both the database and Storage); upgrading to paid only matters at higher usage or for more features
- Postman: the tool to read context from database

## Nice to Know

- **HTTP basics**: request/response, methods (GET/POST), endpoints, headers, body
- **JSON**: the common language APIs speak
- **Basic relational-database concepts**: tables, columns, rows (needed for Supabase tables)
- **Object storage basics**: buckets, files, public vs. signed URLs (needed for Supabase Storage)

## Class Content

- Review from last session, Q&A (10 mins)
- Where Context comes from — three shapes: static text (small FAQ sets can just be pasted into a system prompt; only needs RAG once it's too big or too dynamic to paste), structured dynamic data (Supabase tables), and dynamic files (Supabase Storage); conversation history as a fourth, implicit source (10 mins)
- Design Blazz's dynamic-data schema (10 mins)
- **Build the structured-data side by hand, without n8n**: set up Supabase, create the dynamic-data table for whichever scenario Unit 1 settled on, load in the fake data prepared in Unit 1, then use Postman to call Supabase's REST API directly — insert rows and filter/query them by customer ID (25 mins)
- **Build the file side by hand**: upload a few sample files to a Supabase Storage bucket (whatever file type fits Unit 1's chosen scenario — a diagram, a photo, a document), then use Postman to fetch the one matching a lookup key — same REST-API mechanics as the table, just files instead of rows (20 mins)
- Wrap-up, and confirm Blazz's cleaned-up FAQ text (from Unit 1's homework) is ready to paste into a system prompt next unit (5 mins)

## Deliverables

- Blazz's FAQ text, cleaned up and ready to paste into a system prompt in Unit 3
- A Supabase table loaded with the fake dynamic-customer data decided in Unit 1, verified by inserting and querying rows through direct REST API calls (Postman)
- A Supabase Storage bucket with a few sample files matching Unit 1's chosen scenario, verified by fetching the correct one via direct REST API calls

## Homework

TBD

---

[← Previous: The Three Pillars of an Agent](unit-1.md) ｜ [Next: Building the Agent's Brains and Hands →](unit-3.md)
