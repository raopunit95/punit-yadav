# Case Studies — Punit Yadav

Product work with the reasoning left in: what the problem actually was, what I considered and
rejected, what I chose *not* to build, what it moved, and what I got wrong.

| Case study | Type | Headline result |
|---|---|---|
| [Policy Decoder](./case-studies/policy-decoder.md) | 0→1, self-built prototype → production | ~2,300 leads/month · 19 corporates × 90+ conditions · [live demo](https://raopunit95.github.io/gmc-decoder/) |
| [Dental Procedure Booking](./case-studies/dental-booking.md) | Payments & booking flow | ₹16–17 Cr → ₹27 Cr target · a 7-day build cut from scope |
| [New Services Hub](./case-studies/bottom-nav-hub.md) | Distribution & prioritisation | ~4,000 leads/month at a 40% landing-to-lead rate |
| [CRM Replacement](./case-studies/crm-migration.md) | Platform migration | 350 seats, 300+ GB, zero downtime · pipeline 11,400 → 37,700 records/hour |

---

## Also shipped

**Cashless Hospital Finder** — replaced a lead-capture form losing 80% of users with an interactive
finder taking GPS, pincode or city plus treatment and insurer, returning hospitals ranked by
distance, rating and insurance match. Target: form completion 19% → 45%. ~40 leads/day.
[Live](https://www.medibuddy.in/surgery-care/find-hospitals)

**Condition-to-Department Mapping Tool** — a Retool-backed mapping layer powering site search,
listing and automatic CRM opportunity creation with correct department routing. Uniqueness
validation, case-insensitive and fuzzy matching, an Others fallback, CSV bulk operations, an audit
log and role-based access. Standardised 218 sub-departments across 24 departments.

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
