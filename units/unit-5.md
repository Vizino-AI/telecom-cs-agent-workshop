# Unit 5: Hardening (Error Handling, Rate Limiting, Security, Scalability)

[← Back to course overview](../README.md)

## Learning Objectives

Learn to use a "difficult-customer stress test" mindset to find the system's weak points, and shore up the protections it needs before going live.

## Accounts to Set Up

None (this unit reuses and hardens the services already set up).

## Background Knowledge Needed

- **Rate limiting**: what request throttling is, and why it matters
- **Common security concepts**: least-privilege access, data masking/encryption
- **Basic scalability concepts**: concurrency, load

## Class Content

- Review from last session, Q&A
- Error handling: fallback design for API timeouts/failures, malformed LLM output, and Context lookups that come back empty
- Rate limiting: protecting the agent and backend APIs from being overwhelmed by a single user or a malicious script
- Security: access control and data masking when handling customer PII (phone numbers, billing info)
- Scalability: what to watch for when going from a single test case to Blazz's full company scale
- Run real difficult-customer scenarios as a stress test to validate the hardening above

### 90-Minute Rundown

| Time | Content |
| --- | --- |
| 0:00–0:10 | Review from last session, Q&A |
| 0:10–0:30 | Error handling and fallback design |
| 0:30–0:45 | Rate-limiting design |
| 0:45–1:00 | Security: access control and data masking |
| 1:00–1:15 | Scalability discussion, run the difficult-customer stress test |
| 1:15–1:30 | Final demo, wrap-up |

## Deliverables

A system that has passed the difficult-customer stress test, with error handling, rate limiting, security, and scalability hardening in place; final demo

## Homework

None (this is the last unit — the final demo, wrap-up, and next-steps discussion all happen in class).

---

[← Previous: End-to-End Integration](unit-4.md) ｜ [Back to course overview](../README.md)
