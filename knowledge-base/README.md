# Blazz Knowledge Base

[← Back to course overview](../README.md)

30 short, plain-English help articles that Blake searches with RAG — technical support (Scenario 2) and contracts & cancellation (Scenario 3) in one shared knowledge base. Each article covers one topic and stays under 500 words, so **one article = one chunk**: no text splitting needed.

Upload only the files in [`articles/`](articles/). This README is the fact sheet for writing and checking the articles — don't upload it.

## Fact Sheet

Every article follows these facts. If you add or edit an article, check it against this list first so no two articles contradict each other.

### Equipment (all owned by Blazz, provided while the customer has service)

| Device | Model | Key facts |
|---|---|---|
| Router | BlazzRouter R100 (previous model) | Two Wi-Fi names: `Blazz-XXXX` (2.4 GHz) and `Blazz-XXXX-5G` (5 GHz). 4 Ethernet ports. **Does not** support BlazzMesh Extenders |
| Router | BlazzRouter R200 (current model) | One Wi-Fi name, picks the band automatically. 4 Ethernet ports. Supports up to 3 BlazzMesh Extenders |
| TV box | BlazzBox X150 (previous model) | HD up to 1080p. **Ethernet cable only**. Infrared remote, no pairing |
| TV box | BlazzBox X200 (current model) | Up to 4K. Ethernet cable (recommended) or Wi-Fi. Bluetooth voice remote, must be paired (hold Home + Back for 5 seconds) |
| Wi-Fi extender | BlazzMesh Extender | R200 only. Light: solid green = good, blinking amber = too far from router |

- The router connects the home to the Blazz network through the **Blazz line** (cable from the wall). The BlazzBox gets TV **through the router** — router down means TV down.
- Router sticker (bottom): Wi-Fi name, Wi-Fi password, admin password.
- Router settings page: `192.168.1.1`, log in with the admin password.

### Status lights (same on every router and BlazzBox)

| Light | Meaning | What to do |
|---|---|---|
| Solid green | Working normally | Nothing wrong with the line — problem is Wi-Fi or a device |
| Blinking green | Installing an update | Up to 10 min, don't unplug. Still blinking after 30 min → contact support |
| Blinking amber | Trying to connect | Normal up to 5 min after start. After 10 min → restart once. Still amber 30 min after restart → contact support (technician may be needed) |
| Solid red | No signal (line or device fault) | Restart once. Still red → technician. Can't be fixed at home |
| No light | No power | Check cable and outlet. Still off → replacement device |

The articles say **"amber"** and never "orange" — on purpose. A customer typing "my light is orange" should still find the amber articles, which is exactly the "search by meaning, not keywords" point RAG is meant to demonstrate.

### Restart and reset

- **Restart**: unplug power, wait 30 seconds, plug back in, wait up to 5 minutes. Router first, then BlazzBox. **One restart is enough** — repeating it doesn't help.
- **Factory reset**: hold the Reset pinhole for 10 seconds. Only for a forgotten admin password. Erases Wi-Fi name and password, admin password, guest network, and parental controls. Never used to fix a connection.

### Technician visits

- Book one when: (1) solid red after one restart, (2) blinking amber 30 minutes after a restart, (3) 3+ drops in 7 days even if a restart fixes each one, (4) visible damage to the Blazz line or wall jack.
- Weekdays only, two windows: **9–11 a.m.** or **1–3 p.m.** (matches `technician_availability` in [mock-data.md](../mock-data.md)).
- A Blazz team member confirms every booking → confirmation email. If a slot can't be confirmed, another time is offered.
- Free for Blazz network or equipment faults. Adult (18+) must be home.

### Speed

- Wired speed test: 80%+ of plan speed is normal.
- Peak hours **7–11 p.m.**: can dip, but should stay above 50%.
- Below 50% on more than one wired test → restart router once → still low → contact support.

### Equipment fees (same numbers for accidental damage and unreturned equipment)

Router **$150** · BlazzBox **$100** · BlazzMesh Extender **$75**. Faulty equipment (and faulty remotes) is replaced free, shipped within 2 business days.

### Contract and cancellation

- Contract: **24 months** from service start. After that, month-to-month, no fee to cancel.
- Early cancellation fee: **$20 per full month left** (maximum $460). No fee if month-to-month, or if the customer asks to cancel within **15 days** of the start date.
- Switching plans: no fee, contract end date unchanged, starts next billing month, completed by a Blazz team member (never in chat).
- Pausing: 1–6 months, once every 12 months, **$10/month**, contract end date moves later by the paused months, request 5 business days ahead.
- Cancelling: signed Cancellation Request Form required (chat can't cancel) → confirmation email within 1 business day, with the end date and a prepaid return label → service ends 2 business days after the form arrives → return equipment within **30 days** → final bill about **45 days** after service ends → any credit refunded within 30 days.
- Refunds: only the credit for unused days in the last month. No refunds for service already used.
- The **retention offer** (e.g. three months free) is deliberately **not** in the knowledge base — it lives in the Scenario 3 agent's system prompt, so the agent decides when to offer it instead of RAG surfacing it to anyone who asks.

## Article Index

| # | Title | Category |
|---|---|---|
| 01 | [What the Lights on Your BlazzRouter and BlazzBox Mean](articles/kb-01-status-lights-explained.md) | Status Lights & Troubleshooting |
| 02 | [Blinking Amber Light: Reconnecting vs. Disconnected](articles/kb-02-blinking-amber-light.md) | Status Lights & Troubleshooting |
| 03 | [Solid Red Light: Why It Can't Be Fixed at Home](articles/kb-03-solid-red-light.md) | Status Lights & Troubleshooting |
| 04 | [How to Restart Your BlazzBox](articles/kb-04-restart-blazzbox.md) | Status Lights & Troubleshooting |
| 05 | [How to Restart Your BlazzRouter](articles/kb-05-restart-blazzrouter.md) | Status Lights & Troubleshooting |
| 06 | [The Light Is Still Wrong After a Restart: What to Do Next](articles/kb-06-light-still-wrong-after-restart.md) | Status Lights & Troubleshooting |
| 07 | [When to Book a Technician Visit](articles/kb-07-when-to-book-technician.md) | Status Lights & Troubleshooting |
| 08 | [Slow Internet: Common Causes and What to Check](articles/kb-08-slow-internet.md) | Internet Connection & Speed |
| 09 | [Wi-Fi Keeps Cutting In and Out: Check Where Your Router Is](articles/kb-09-wifi-cutting-in-and-out.md) | Internet Connection & Speed |
| 10 | [Weak Wi-Fi in Some Rooms: BlazzMesh Extenders](articles/kb-10-blazzmesh-extenders.md) | Internet Connection & Speed |
| 11 | [Why a Wired Connection Is More Stable Than Wi-Fi](articles/kb-11-wired-vs-wifi.md) | Internet Connection & Speed |
| 12 | [Is Slower Internet in the Evening Normal?](articles/kb-12-evening-slowdown.md) | Internet Connection & Speed |
| 13 | [Mobile Data Works but Home Wi-Fi Doesn't: What's Wrong?](articles/kb-13-mobile-data-works-wifi-doesnt.md) | Internet Connection & Speed |
| 14 | [How to Change Your Wi-Fi Name and Password](articles/kb-14-change-wifi-name-password.md) | Equipment & Network Settings |
| 15 | [Forgot Your Router Admin Password?](articles/kb-15-forgot-admin-password.md) | Equipment & Network Settings |
| 16 | [How to Set Up a Guest Wi-Fi Network](articles/kb-16-guest-wifi.md) | Equipment & Network Settings |
| 17 | [How to Use Parental Controls to Limit Internet Time](articles/kb-17-parental-controls.md) | Equipment & Network Settings |
| 18 | [Software (Firmware) Updates: Why They Matter and How They Work](articles/kb-18-firmware-updates.md) | Equipment & Network Settings |
| 19 | ["Signal Lost" Message on Your BlazzBox: What It Means](articles/kb-19-signal-lost-message.md) | BlazzBox & TV |
| 20 | [TV Remote Not Working or Won't Pair With Your BlazzBox](articles/kb-20-remote-not-working.md) | BlazzBox & TV |
| 21 | [Pixelated or Frozen TV Picture: Common Causes](articles/kb-21-pixelated-frozen-picture.md) | BlazzBox & TV |
| 22 | [HDMI Problems Between Your BlazzBox and TV](articles/kb-22-hdmi-problems.md) | BlazzBox & TV |
| 23 | [Three Things to Check Before You Start Troubleshooting](articles/kb-23-three-things-to-check-first.md) | Diagnosis & Support Policy |
| 24 | [When to Replace Equipment Instead of Troubleshooting](articles/kb-24-replace-equipment.md) | Diagnosis & Support Policy |
| 25 | [How Blazz Sorts Technical Problems: Internet, TV, or Equipment](articles/kb-25-how-problems-are-sorted.md) | Diagnosis & Support Policy |
| 26 | [Your Blazz Contract and Early Cancellation: The Basics](articles/kb-26-contract-basics.md) | Contracts & Cancellation |
| 27 | [How the Early Cancellation Fee Is Calculated](articles/kb-27-early-cancellation-fee.md) | Contracts & Cancellation |
| 28 | [Before You Cancel: Switching Plans or Pausing Your Service](articles/kb-28-switch-or-pause-before-cancelling.md) | Contracts & Cancellation |
| 29 | [Returning Your Equipment After You Cancel](articles/kb-29-return-equipment.md) | Contracts & Cancellation |
| 30 | [How to Cancel: From Request to Final Bill](articles/kb-30-how-to-cancel.md) | Contracts & Cancellation |
