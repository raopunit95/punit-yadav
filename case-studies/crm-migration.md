# CRM Replacement

**350 seats, two systems retired, zero downtime — on an operation making 5,000 calls a day**

Role: Customer-side owner — requirements, data model, integrations, data cleansing, cutover
Duration: ~3 months · System of record from 1 July 2026

---

## Context

Every lead MediBuddy's surgery business receives lands in a CRM, and roughly 350 people — care
coordinators, clinical coordinators, scheduling, finance operations — spend their entire working day
inside it. The business makes **~5,000 outbound calls a day, about 450,000 minutes a month**, through
that system.

I had built the outgoing platform. Over four years it had gone from an unstructured instance to the
operating system of the business: 250+ data points, trigger logic on field change, task and
follow-up rules, ownership routing, 62+ automation workflows, five internal tools, and a lifecycle
communication layer across 22 email and 14 WhatsApp touchpoints.

Then the company chose to replace it.

## The situation I was actually in

Migrating a system you built yourself has one advantage and one trap. The advantage is that you know
where every body is buried. The trap is that you're the only one who does — which means if you don't
write it down, it doesn't survive the migration.

Two things made this harder than a normal cutover:

**The vendor's contract excluded data cleansing.** In writing: the customer is responsible for
preparing, cleaning and validating data before handing it over; the vendor performs no cleansing and
relies entirely on what it receives. That is a completely reasonable commercial position, and it
meant the quality of a four-year-old data estate — **4.37 million opportunity records and 21.3
million call records** — was my problem, not theirs.

**There is no maintenance window.** A business making five thousand calls a day cannot pause. The
cutover had to be a switch, not a shutdown.

## What I found in the vendor's requirements document

Reading the BRD line by line, **two lines of business were missing from it entirely.** They existed
in the outgoing system, they had live data and active users, and they simply weren't in the scope
document — the kind of omission that surfaces three weeks after go-live as a team discovering their
work has nowhere to go.

I raised it before build. Catching it after would have meant an emergency scope addition against a
signed statement of work.

## What I owned

- **Data model and configuration** on the new platform — objects, fields, stages, role-specific forms
  for each of the four teams, task generation between them, and ownership rules.
- **Integrations** — cloud telephony for calls, the lead-distribution layer, WhatsApp, email delivery
  and the core platform backend. Engineering support was scoped to lead ingestion and the email API;
  everything low-code was mine.
- **Data preparation, cleansing and validation** across the full historical estate, plus **300+ GB of
  documents against 76,903 opportunity records** moved into object storage.
- **Business rules** — deduplication keys, cooling-off logic, source priority, and the stage
  definitions the whole funnel reports against.
- **Cutover** into a live operation.

## The migration pipeline

The document migration was the part with real engineering risk: hundreds of gigabytes of
prescriptions, insurance documents, approvals, discharge summaries and bills, each attached to a
specific record, none of which could be lost or misfiled.

**I authored the original automation workflow that became the technical basis for the whole
migration.** It was later re-implemented in Python for the first phase, then redesigned into a
concurrent assembly-line architecture — lookup, collect, back up, confirm, run in parallel across
records — for the second.

| Phase | Throughput |
|---|---|
| First run | ~11,400 records/hour |
| Redesigned run | **~37,700 records/hour** |

A 3.3× improvement, on the same pipeline, by changing its shape rather than its logic.

## Result

| | |
|---|---|
| Seats migrated | ~350 |
| Legacy systems retired | 2 |
| Documents migrated | 300+ GB across 76,903 records |
| Historical estate handled | 4.37M opportunities, 21.3M call records |
| Business interruption | **None** |
| System of record from | 1 July 2026 |

The programme was held to three success criteria: **one system of record** with no shadow
spreadsheets for standard operations, **faster agent onboarding** than the previous three-month
ramp, and **leadership funnel visibility** through a hierarchy roll-up. All three shipped.

Alongside the migration I requested and validated a lead-creation cooldown rule that went live in
August 2026, and rewrote deduplication and source-priority logic so a higher-priority inbound payload
updates an existing record rather than spawning a duplicate — **duplicate protection rose from 180 to
290 per day and reverse duplicates fell from 20% to 15%.**

## What I'd do differently

- **I was the single point of failure and I let that stand too long.** Because I'd built the outgoing
  system, most of its undocumented behaviour lived in my head. That made me fast and made the
  programme fragile. I'd write the behavioural documentation first next time, even though it feels
  like the slowest possible way to start.
- **Data cleansing deserved its own workstream and its own estimate.** It was the largest hidden cost
  in the programme and it was treated as a task inside the migration rather than a project beside it.
  The vendor's contract told me exactly how much work it was going to be and I under-planned it
  anyway.
- **I read the BRD closely enough to find the missing lines of business — but only once.** A second
  structured review, with the team leads who'd have to live in the new system, would probably have
  surfaced more.
- **The throughput redesign should have come first.** The first phase ran at 11,400 records an hour
  because that was the obvious implementation. The concurrent design wasn't a new insight by the
  second phase; it was one we could have reached before spending the first run.

---

**Demonstrates:** platform migration and cutover planning · vendor scope negotiation and BRD review ·
data modelling, cleansing and validation at scale · pipeline throughput design · delivering against a
defined success bar on a live operation.
