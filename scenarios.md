# Three Core Customer-Service Scenarios

[← Back to course overview](README.md)

These three scenarios stay close to real telecom business needs and together cover tool calling, static-knowledge lookups, and human-in-the-loop — a great script to build the multi-agent implementation around. Prefer these three scenarios when designing fake data, test cases, or demos; [Unit 1](units/unit-1.md)'s homework can point the student toward these three directions when designing Blazz's fake data.

## Scenario 1: Billing Inquiry & Plan Upsell

The most basic, most common telecom scenario — good for testing an agent's logical reasoning and data-lookup ability.

**Customer message**: "Why did my bill jump to over $2,000 this month?"

**Flow**:

1. Intent classification: the router agent classifies this as a billing question and hands off to the "billing support agent"
2. Call a tool (API): trigger an API call to look up this customer's billing detail for the month (the fake billing table built in [Unit 2](units/unit-2.md) in Supabase)
3. Analyze & respond: discover the customer used roaming data abroad, and explain the source of the charge
4. Upsell: based on the customer's frequent-travel pattern, proactively recommend the "$500/month global roaming unlimited" plan

**n8n highlight**: practice having the agent call Supabase to fetch fake customer data, and demonstrate the AI's ability to analyze that data.

### Related SOP: Plan Change Request

A natural extension once the upsell lands — the customer says "okay, switch me to that plan." Blazz's real billing system can't be changed by the bot, and working out eligibility or the right plan is a judgment call — so the agent doesn't attempt any of it, not even partially. It just recognizes the request and flags it for a human.

**Why not let the agent handle any part of it?** A plan change touches billing and contract terms — get it wrong (misheard plan, wrong customer, a bundled promo that silently voids) and it's a real financial mistake, not an undo-able chat message. This is exactly the class of "account-altering" decision [Unit 5](units/unit-5.md)'s guardrails lesson is about: it always routes to a human, no matter how confident the Model sounds — the agent doesn't get partial credit for checking eligibility correctly if it still can't be trusted to execute.

1. **Recognize the request**: as soon as the customer confirms they want to switch plans, stop there — no eligibility check, no plan recommendation, no deciding which plan fits
2. **Set expectations**: tell the customer a human will follow up on the request; never imply it's already done
3. **Flag it via email**: send an email to Blazz's internal customer-service mailbox (e.g. `planchanges@blazz.internal`) with the customer's identity and a plain-language summary of the request, headed with a clear **`ACTION REQUIRED`** marker so a human can't miss it and takes over from there — the same Email Tool pattern as Scenario 3's cancellation form, just a much simpler email: no recommended plan, no eligibility math, only the flagged summary

This still reuses the Email Tool — the simplification is entirely in what the agent decides before sending it, not whether it sends anything.

## Scenario 2: Internet Outage Troubleshooting

Shows a Supabase Storage document lookup, a case the AI genuinely can't resolve alone, and human-in-the-loop with real interactive Slack buttons — not just a notification.

**Customer**: David Kim (see [mock-data.md](mock-data.md) — Toronto, ON, matches technicians Priya Sharma and Marco Ricci's availability)

**Customer message**: "My internet keeps dropping — I've rebooted three times already and it's still not working!"

**Flow**:

1. **Intent classification**: the router agent classifies this as a technical issue and hands off to the technical-support agent
2. **Knowledge lookup**: a Tool call fetches the troubleshooting FAQ from Supabase Storage for the standard steps
3. **Initial troubleshooting**: the FAQ's steps assume the customer *hasn't* already rebooted — David has, three times, so the agent has nothing left to try from the FAQ. This is the point of the scenario: the AI genuinely runs out of road, not a scripted "give up" step
4. **Check technician availability**: rather than just escalating blind, the agent queries `technician_availability` for David's region (Toronto, ON) and offers 2–3 real slots: *"I found technicians available Tuesday 9–11am or Thursday 1–3pm — which works for you?"*
5. **Customer picks a slot**: no database write yet — the chosen slot's id, David's identity, and the issue description just ride along in the workflow's own execution data
6. **Escalate with actionable buttons, not just a message**: n8n posts to `#blazz-cs-escalations` with the customer, region, issue, and proposed slot — plus two real Slack action buttons: **Confirm** and **Propose Other Time** (n8n's Slack "Send and Wait for Response" node supports custom button labels, mapping directly onto its native two-button approval pattern — no fallback needed here). This is a hard-coded branch, not a Model decision — the AI Agent isn't involved from here until it needs to relay the outcome
7. **Human clicks a button** — two branches, each a plain `technician_availability` update, no separate tracking table needed:
   - **Confirm** → `UPDATE technician_availability SET status = 'booked' WHERE id = <slot>`; n8n also sends David a confirmation email (technician, date, time) in parallel, in case he's no longer in the chat; the AI tells him in-chat too, if he still is
   - **Propose Other Time** → `UPDATE technician_availability SET status = 'unavailable' WHERE id = <slot>` (it turned out this one can't actually be honored); the AI goes back to David, tactfully explains that, and asks whether one of the remaining slots works instead (loop back to step 4)

**n8n highlight**: built end to end in [Unit 3](units/unit-3.md) — the interactive Slack buttons and the loop-back on "Propose Other Time" are what make this more than "post a message and wait."

## Scenario 3: Cancellation & Retention

A more advanced scenario that tests the AI's emotional awareness and negotiation skills — good for [Unit 5](units/unit-5.md)'s hardening/difficult-customer stress test.

**Customer message**: "Your signal is terrible! I want to file a complaint! I want to cancel and get a refund — send me the form right now!"

**Flow**:

1. Intent & sentiment classification: detect strong negative sentiment and cancellation intent
2. Knowledge lookup: a Tool call fetches the contract terms from Supabase Storage to calculate the early-termination fee the customer would owe
3. De-escalate & retain (hidden offer): don't hand over the cancellation form immediately — first explain the termination fee, then offer a hidden retention deal (e.g. three months free) to try to win back the customer
4. Automated tool (email): if the customer still insists on cancelling, trigger an email node to automatically send the cancellation request form

**n8n highlight**: test the "retention floor" the AI is instructed to hold in its prompt, and wire up the email node to complete the form-sending step.

### Branch: Customer Demands a Human

Sometimes de-escalation itself is the wrong move — a customer who's truly furious and explicitly says "I don't want to talk to a bot, get me a real person" should be honored immediately, not met with another round of retention logic. Continuing to argue at that point reads as the bot ignoring them, which makes things worse, not better.

1. **Detect the explicit ask**: recognize "give me a human" / "I want to talk to a person" as its own trigger, separate from sentiment or cancellation intent — it overrides the retention flow rather than feeding into it
2. **Fall back immediately**: send an email to Blazz's call center with three things:
   - the customer's verified identity
   - the full conversation transcript
   - a short AI-generated **summary** of the conversation, so the human isn't stuck reading a long heated back-and-forth cold before they can respond
3. **Tell the customer**: confirm a human has been looped in and roughly when to expect a reply — don't keep negotiating in the meantime

This is the same escalation pattern as [Unit 4](units/unit-4.md)'s confidence-based fallback (identity + transcript to the call center), just triggered by an explicit request instead of a low confidence score, with a summary added on top. Worth formalizing as a general rule in Unit 4's triage layer, not just a Scenario 3 special case — an explicit "get me a human" should short-circuit any scenario, not only cancellation.

---

Together these three examples cover looking up data, checking reference text, escalating for help, and sending email — exactly what shows the student how powerful an agent becomes once it has "hands and feet."
