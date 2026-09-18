# Unit 5: Hardening (Error Handling, Rate Limiting, Security, Scalability)

[← Back to course overview](../README.md)

## Learning Objectives

Learn to use a "difficult-customer stress test" mindset to find the system's weak points, and shore up the protections it needs before going live.

## Setup

None.

## Nice to Know

- **Rate limiting**: what request throttling is, and why it matters
- **Common security concepts**: least-privilege access, data masking/encryption
- **Basic scalability concepts**: concurrency, load

## Class Content

- Review from last session, Q&A (10 mins)
- Error handling: fallback design for API timeouts/failures, malformed LLM output, and Context lookups that come back empty (20 mins)
- Rate limiting: protecting the agent and backend APIs from being overwhelmed by a single user or a malicious script (15 mins)
- Security: access control and data masking when handling customer PII (phone numbers, billing info) (15 mins)
- Scalability: what to watch for when going from a single test case to Blazz's full company scale; run real difficult-customer scenarios as a stress test to validate the hardening above (15 mins)
- Final demo, wrap-up (15 mins)

## Deliverables

A system that has passed the difficult-customer stress test, with error handling, rate limiting, security, and scalability hardening in place; final demo

## Homework

None.

---

[← Previous: End-to-End Integration](unit-4.md) ｜ [Back to course overview](../README.md)
