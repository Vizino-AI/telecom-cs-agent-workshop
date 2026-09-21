# Three Core Customer-Service Scenarios

[← Back to course overview](README.md)

These three scenarios stay close to real telecom business needs and together cover RAG, API lookups, and human-in-the-loop — a great script to build the multi-agent implementation around. Prefer these three scenarios when designing fake data, test cases, or demos; [Unit 1](units/unit-1.md)'s homework can point the student toward these three directions when designing Blazz's fake data.

## Scenario 1: Billing Inquiry & Plan Upsell

The most basic, most common telecom scenario — good for testing an agent's logical reasoning and data-lookup ability.

**Customer message**: "Why did my bill jump to over $2,000 this month?"

**Flow**:

1. Intent classification: the router agent classifies this as a billing question and hands off to the "billing support agent"
2. Call a tool (API): trigger an API call to look up this customer's billing detail for the month (the fake billing table built in [Unit 2](units/unit-2.md) in Supabase)
3. Analyze & respond: discover the customer used roaming data abroad, and explain the source of the charge
4. Upsell: based on the customer's frequent-travel pattern, proactively recommend the "$500/month global roaming unlimited" plan

**n8n highlight**: practice having the agent call Supabase to fetch fake customer data, and demonstrate the AI's ability to analyze that data.

## Scenario 2: Internet Outage Troubleshooting

Shows RAG (knowledge-base retrieval) combined with human-in-the-loop (human handoff).

**Customer message**: "My internet keeps dropping — I've rebooted three times already and it's still not working!"

**Flow**:

1. Intent classification: the router agent classifies this as a technical issue and hands off to the "technical support agent"
2. Knowledge retrieval (RAG): search the vector database for "internet outage FAQ" to find the standard troubleshooting steps (e.g. checking the set-top box's status lights)
3. Initial troubleshooting: walk the customer through checking the light; if they report a red light, conclude it can't be resolved via software
4. Escalate (Slack): trigger n8n's Wait and Slack nodes to send the conversation history to a human supervisor
5. Human takes over: the supervisor clicks "approve dispatch" in Slack, and the AI tells the customer a technician has been scheduled

**n8n highlight**: [Unit 3](units/unit-3.md)'s RAG knowledge base and [Unit 4](units/unit-4.md)'s Slack human-in-the-loop both shine here.

## Scenario 3: Cancellation & Retention

A more advanced scenario that tests the AI's emotional awareness and negotiation skills — good for [Unit 5](units/unit-5.md)'s hardening/difficult-customer stress test.

**Customer message**: "Your signal is terrible! I want to file a complaint! I want to cancel and get a refund — send me the form right now!"

**Flow**:

1. Intent & sentiment classification: detect strong negative sentiment and cancellation intent
2. Knowledge retrieval (RAG): look up the contract knowledge base to calculate the early-termination fee the customer would owe
3. De-escalate & retain (hidden offer): don't hand over the cancellation form immediately — first explain the termination fee, then offer a hidden retention deal (e.g. three months free) to try to win back the customer
4. Automated tool (email): if the customer still insists on cancelling, trigger an email node to automatically send the cancellation request form

**n8n highlight**: test the "retention floor" the AI is instructed to hold in its prompt, and wire up the email node to complete the form-sending step.

---

Together these three examples cover looking up data, searching documents, escalating for help, and sending email — exactly what shows the student how powerful an agent becomes once it has "hands and feet."
