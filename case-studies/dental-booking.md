# Dental Procedure Booking

**A deposit-and-settlement flow for a service whose price isn't knowable at booking**

Role: PM (owner) — PRD, scoping, cross-team decision-making · Target: ₹16–17 Cr/yr → ₹27 Cr (+75%)

---

## Context

MediBuddy's dental line runs at a ₹16–17 Cr annual run rate. Corporate customers hold dental wallet
balances they've already been given — and a large share of those balances go unspent. The users
aren't price-sensitive at the margin; they're friction-sensitive. There was no way to book a dental
procedure in the app at all. Every booking went through an operations team punching orders manually.

The opportunity was not new demand. It was **removing the manual step between an existing entitlement
and a completed procedure.**

## The hard problem

Dental procedures share an awkward property with a lot of services: **the final price isn't knowable
at the time of booking.** What the dentist finds during the procedure changes the work, which changes
the bill, which changes the covered amount and the copay.

That single fact rules out the obvious design — take payment, confirm the order, done — and it's the
constraint the whole spec is built around.

## Options I considered

| Option | Why I didn't pick it |
|---|---|
| Collect the full estimated amount at booking | Over-collects on most bookings and under-collects on the rest. Refunds become the default path rather than the exception, and the user's first experience of the product is a number that turns out to be wrong. |
| Collect nothing; settle entirely after the procedure | Zero commitment at booking means no-shows, and the operations cost of chasing payment after a service is already delivered is the reason the manual process existed. |
| Show a price range and collect the midpoint | Still wrong most of the time, and it makes the displayed range look like a quote — which invites a dispute at settlement. |
| **Flat deposit at booking, delta settled after** ← chose this | A fixed ₹499 token creates commitment, is small enough not to require a real quote, and separates the booking decision from the pricing decision. Travel and hospitality settle this way for the same reason. |

**The price shown to the user is deliberately decoupled from the amount collected.** The catalog can
display a median price or a range for orientation, and the amount charged is the flat token
regardless. That means the display is informational, not contractual — so improving price accuracy
later never becomes a billing change.

## The scope cut I'm most pleased with

The original design called for a real-time rule engine evaluating, at the moment of booking:
per-SKU coverage, applicable copay, and capping — with adjudication groups modelled on an existing
system. Engineering estimated it at **7 person-days**, and it was the single largest item in the
build.

I pushed back on the requirement rather than the estimate. The question I asked was: *what does the
user actually need to know before they commit?* The answer was one bit of information — **is dental
procedure booking available to me at all under my employer's plan?** Everything else — which
procedures are covered, at what copay, up to what cap — is only knowable once the procedure is done,
and operations already determine it at settlement.

So the real-time rule engine became a **single corporate-eligibility check**, and coverage
adjudication moved to the point where the information actually exists. Same user outcome, seven
engineering days returned to the build.

## What the spec covers

**22 requirements, phased: 18 into a ~41 person-day V0**, with V1 and V2 explicitly deferred and each
deferral reasoned in writing.

| Area | Specified |
|---|---|
| Entry points | A dental hub, a redirect from a completed consult order (which inherits provider context and skips a screen), and a deep link from lifecycle communications |
| Supply eligibility | Not every clinic that does consults does procedures — capability flags live on provider master data and are checked at render time |
| Catalog | 470 SKUs, with a defined ownership model for who can change a price and who can add a procedure |
| Payment | Flat ₹499 deposit at booking via wallet hold or payment gateway; a second payment link for the delta once operations finalise the amount; automatic refund if over-collected |
| Data model | Multiple requests roll up under one order; deletion of a procedure isn't supported at request level and requires cancel-and-recreate — a constraint I documented rather than papered over |
| Lifecycle | Seven events covering user, operations and automatic cancellation, date change with refund-and-re-hold, post-procedure delta, and prescription replacement |
| Operations | A settlement dashboard replacing a legacy internal tool, with a full audit trail on every finalisation |
| Analytics & sync | Screen-level event tracking through the booking funnel; hourly order sync into the CRM |

**Explicitly out of V0:** partner-side calendar sync, in-app chat with operations, self-service
procedure edits, and provider-hierarchy mapping. Each is a real request from a real stakeholder,
each deferred with a stated reason.

## Running it across nine teams

Engineering, corporate engineering, product operations, supply network, finance operations, account
management, analytics, legal/claims and the low-code team all owned a piece of this.

The mechanism that kept it moving was a **decisions-made and questions-open register maintained
through every revision** — each decision recorded with what was chosen and what it superseded, each
open question named with why it matters and who owns it. By v2.2 the register showed five decisions
resolved since the previous draft and five questions still open, each with an owner.

That register is the part of the document I'd defend hardest. Specs don't stall because people
disagree; they stall because nobody can remember what was already agreed.

## Status

Development kickoff September 2026. Target: **₹27 Cr annual run rate, a 75% increase.**

Success metrics defined up front: booking requests created, orders completed versus created split by
entry point, revenue from the channel, and auto-cancellation rate.

## What I'd do differently

- **The ₹499 figure changed twice** during drafting — from a working range, to an ₹800 minimum
  bookable value, to a flat ₹499 — and for one revision the two rules contradicted each other in the
  same document. I should have forced that decision to a single owner earlier instead of letting two
  framings coexist.
- **I still don't know how often scope shrinks after a consult.** That number sizes how often the
  cancel-and-recreate path gets used, and it's the open question most likely to turn into an
  operations complaint after launch. I should have pulled it from historical data rather than
  carrying it as an open item.
- **Keeping all 470 SKUs as-is** was the right call for shipping speed, but it means the first
  user-facing picker will show a catalog nobody has audited. The cleanup is deferred, not cancelled,
  and I'd rather have scoped a minimal version of it into V0.

---

**Demonstrates:** designing around a hard business constraint · cutting scope by challenging a
requirement rather than an estimate · payment, cancellation and refund policy design · data-model
tradeoffs documented honestly · driving decisions across nine teams.
