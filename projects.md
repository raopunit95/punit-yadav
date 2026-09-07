# Case Studies — Punit Yadav

Product work with the reasoning left in: what the problem actually was, what I considered and
rejected, what I chose *not* to build, what it moved, and what I got wrong.

| Case study | Type | Headline result |
|---|---|---|
| [Cashless Hospital Finder](./case-studies/hospital-finder.md) | 0→1, self-built prototype → production | **~50 leads/day → ~30 surgeries/month → ₹21 lakh/month** · [live](https://www.medibuddy.in/surgery-care/find-hospitals) · [source](https://github.com/raopunit95/surgery-network-finder) |
| [Policy Decoder](./case-studies/policy-decoder.md) | 0→1, self-built prototype → production | ~2,300 leads/month · 19 corporates × 90+ conditions · [live](https://www.medibuddy.in/surgery-care/policy) *(signed-in)* · [public demo](https://raopunit95.github.io/gmc-decoder/) |
| [Dental Procedure Booking](./case-studies/dental-booking.md) | Payments & booking flow | ₹16–17 Cr → ₹27 Cr target · a 7-day build cut from scope |
| [New Services Hub](./case-studies/bottom-nav-hub.md) | Distribution & prioritisation | ~4,000 leads/month at a 40% landing-to-lead rate |
| [CRM Replacement](./case-studies/crm-migration.md) | Platform migration | 350 seats, 300+ GB, zero downtime · pipeline 11,400 → 37,700 records/hour |

---

## Cashless Hospital Finder — live in production

**[medibuddy.in/surgery-care/find-hospitals](https://www.medibuddy.in/surgery-care/find-hospitals)**

A patient who needs surgery wants one answer: *where can I have this done, near me, cashless on my
insurance?* Insurer network lists are PDFs organised by city. Hospital directories are organised by
medical department. Neither is organised by the thing the patient actually types. The lead-capture
form standing in for an answer was losing 80% of the users who reached it.

Replaced it with an interactive finder — GPS, pincode or city, plus treatment and insurer —
returning hospitals ranked by distance, rating and insurance panel, then the doctors at the chosen
hospital who perform that specific procedure.

| Metric | Value |
|---|---|
| Leads | ~50 / day |
| Surgeries booked | ~30 / month |
| Booked value | ₹21 lakh / month (~₹2.5 Cr annualised) |
| Target set | Form completion 19% → 45% |

**The interesting problem.** Patients search for a *condition*; hospitals are filed by *department*.
Someone types "Piles", the network says "General Surgery", and nothing connects the two. Solving it
meant a mapping layer — 218 sub-departments across 24 departments — and learning that a department
is a filing category, not a matching key: the catch-all "Aesthetic" covers plastic surgery,
dermatology, cosmetology and hair transplants, so routed naively a nose job matched hair clinics.

**How it was de-risked.** I built the working prototype myself and published it, to prove the
distance ranking and the condition-to-speciality matching before asking for an engineering sprint.
648 hospitals, 3,547 doctors, 218 surgeries, 144 cities, 36 insurers — a static site with zero
dependencies. [Source](https://github.com/raopunit95/surgery-network-finder) ·
[demo](https://raopunit95.github.io/surgery-network-finder/)

**[Read the full case study →](./case-studies/hospital-finder.md)**

---

## Also shipped

**Condition-to-Department Mapping Tool** — a Retool-backed mapping layer powering site search,
listing and automatic CRM opportunity creation with correct department routing. Uniqueness
validation, case-insensitive and fuzzy matching, an Others fallback, CSV bulk operations, an audit
log and role-based access. Standardised 218 sub-departments across 24 departments — the same layer
the Cashless Hospital Finder searches against.

**Automated consult booking** — a pincode-to-nearest-hospital API plus a full conversational booking
flow. ~10 bookings/day with no human in the loop, 60–70 surgeries/month — equivalent to 5–6 agents
of capacity at 11–12 surgeries per agent per month.

**Closing the post-surgery data loop** — once a patient's record moved into the CRM it left the app
ecosystem, so completed surgeries never flowed back. Specified a discharge order surfacing bills,
invoices, discharge summaries and prescriptions in-app across 3,300+ surgeries.

**Vaccination programme reconciliation** — owned the data layer of a nationwide corporate programme
delivered by field teams: 1,340 camps, 175 corporate accounts, 104 cities, 249,000 doses against
₹27.9 Cr of billing. The three-way reconciliation I built ran before every invoice; 308 of 838
dual-source camps disagreed, and resolving 7,666 doses of variance protected ~₹72 lakh in billing
accuracy.

**In pilot** — an AI lead-qualification model scoring intent 0–10, designed to qualify the same
~6,000 leads/month with 60% of current agent headcount. Projected distribution: 15% above 7, 50%
between 4 and 7, 35% below 4.

---

## The format

Every write-up follows the same six sections, because that's the order the question actually gets
asked in:

1. **Context** — the business, the number, why this mattered now
2. **Problem** — what I learned from users and data, and how I sized it
3. **Options** — what I considered, and *what I chose not to build and why*
4. **What I shipped** — scope, phasing, who I worked with
5. **Result** — the metric, the baseline, the window, and how it was attributed
6. **What I'd do differently** — the honest part
