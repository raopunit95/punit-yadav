# Punit Yadav
**Product Manager — Consumer Marketplace, Booking Flows & Growth**

Gurugram, India · puneetyadav95@gmail.com · +91 70467 29984
[LinkedIn](https://linkedin.com/in/punit-yadav-2ab6a013b) · [GitHub](https://github.com/raopunit95) · [Portfolio](https://raopunit95.github.io/punit-yadav/)

---

## Summary

Product Manager with 7 years of experience building consumer booking and marketplace products,
5 of them at MediBuddy where I own the demand side of a ₹150 Cr surgery business running ~1,500
procedures and ~₹11 Cr a month. Five PRDs authored and shipped to development, four systems built
from zero, and end-to-end ownership of the funnel: discovery, spec, catalog and pricing, payment and
cancellation flows, lifecycle CRM, and the analytics that prove it worked. I write SQL, instrument
my own events, and ship working prototypes when that's the fastest way to learn whether an idea
deserves a sprint.

**Selected impact** — Cashless Hospital Finder live in production at ~50 leads/day → ~30
surgeries/month → ₹21 lakh of booked value monthly · Funnel entries 90k → 150k/month · ~2,300
leads/month from insurance transparency · 60–70 surgeries/month booked with no human involvement ·
350-seat CRM migration delivered · ₹72 lakh of billing variance reconciled

---

## Experience

### MediBuddy — Gurugram
*India's largest digital healthcare platform · Surgery line grew ₹100 Cr → ₹130 Cr → ₹150 Cr; 95% corporate mix*

**Senior Manager, Product** · Jul 2026 – Present
**Analyst III / Analyst II, Surgery New Initiatives** · Apr 2023 – Jun 2026
**Manager / Management Trainee, Corporate Business** · Jun 2021 – Mar 2023

Own the acquisition-to-surgery funnel and the dental booking product. Squad of one backend engineer,
one frontend engineer and one designer; I instrument and build all product analytics myself.

#### Product ownership — 5 PRDs authored, 1 contributed

- **[Dental Procedure Booking](./case-studies/dental-booking.md)** (owner). Targeting growth from a
  ₹16–17 Cr annual run rate to ₹27 Cr (+75%) by converting dormant corporate wallet balances into
  booked procedures. Scoped and phased 22 requirements into an 18-item V0 at ~41 person-days:
  a 470-SKU catalog, a flat ₹499 deposit with post-procedure delta collection or refund, provider
  eligibility rules, the request-to-order data model, seven lifecycle events, auto-cancellation, an
  operations settlement dashboard, event tracking and hourly CRM sync. Drove decisions across nine
  teams with an explicit decisions-made and questions-open register.
- **Removed a 7 person-day rule-engine build from scope** by reducing real-time evaluation to a
  single corporate-eligibility check and moving coverage, copay and capping to operations at
  settlement — same outcome, a fraction of the effort.
- **[Policy Decoder](./case-studies/policy-decoder.md)** (owner). Built the
  [public prototype](https://raopunit95.github.io/gmc-decoder/) myself to validate demand, then
  shipped in-app across 19 corporate accounts and 90+ conditions each —
  [live in the MediBuddy app](https://www.medibuddy.in/surgery-care/policy) *(signed-in users)*.
  Designed the access-control model — corporate email domain match plus OTP for unauthenticated
  users — to prevent leakage of corporate policy data between accounts. ~30 leads/day from the
  decoder page; ~2,300 leads/month across all insurance-transparency entry points.
- **[Cashless Hospital Finder](https://www.medibuddy.in/surgery-care/find-hospitals)** (owner) —
  **live in production**. Replaced a lead-capture form losing 80% of users with an interactive
  finder taking GPS, pincode or city plus treatment and insurer, returning hospitals ranked by
  distance, rating and insurance panel, then the doctors at that hospital who perform the specific
  procedure. **~50 leads/day converting to ~30 surgeries/month — ₹21 lakh of booked value monthly
  (~₹2.5 Cr annualised)**, against a target of moving form completion from 19% to 45%. I built the
  working prototype myself first, to prove the distance ranking and the condition-to-speciality
  matching before committing an engineering sprint:
  [source](https://github.com/raopunit95/surgery-network-finder) ·
  [demo](https://raopunit95.github.io/surgery-network-finder/).
- **[New Services bottom-navigation hub](./case-studies/bottom-nav-hub.md)** (owner). Analysed ~1.5M
  monthly bottom-nav taps to justify replacing the lowest-performing icon (807 taps) with a services
  hub, with entity-level configurability, Snowplow tracking and homepage fallback on broken deep
  links. Now reaches ~180k unique users monthly; surgery converts ~10,000 monthly landings into
  ~4,000 leads at a 40% landing-to-lead rate.
- **Condition-to-Department Mapping Tool** (owner). Specified a Retool-backed mapping layer powering
  surgery page search, listing and automatic CRM opportunity creation with correct department
  routing — uniqueness validation, case-insensitive and fuzzy matching, an Others fallback, CSV bulk
  operations, an audit log and role-based access. Standardised 218 sub-departments across 24
  departments — the same mapping layer the hospital finder searches against, so a patient searching
  a condition reaches hospitals filed under a department.
- **Unified Network & Order Management** (contributor). Defined the CRM integration fields, API
  contract and sync logic for an engineering-led programme unifying surgery OPD and in-clinic
  consult networks, using the CRM opportunity ID as the primary key for end-to-end order continuity.

#### Growth, conversion and cross-sell

- **Grew funnel entries 90,000 → 150,000/month, a 1.4× lead increase at flat acquisition cost**, by
  opening entry points where patient intent already existed — bottom navigation, claims page,
  benefits surface and corporate-specific surgery icons — rather than buying traffic.
- **Opened cross-vertical lead capture** from lab tests, medicine orders and offline OPD
  consultations into the surgery funnel, converting existing platform traffic into surgery demand
  instead of paying to acquire it again.
- **Increased condition-page conversion 1.2% → 1.4%** and added ~1,200 leads/month by shipping a
  no-code CMS that let marketing publish pages without an engineering sprint.
- **Recovered dental payment drop-offs** by creating leads from users abandoning at the payment
  step — a 5% revenue uplift on the dental line.
- **Deliberately traded volume for quality** by replacing misleading symptom options with clinically
  correct terms, knowingly accepting a loss of 15–20 leads/day because those leads never converted.
- **Ran experiments including the losses** — an animated creative variant reduced click-through from
  3.5% to 2.7%, so it was discontinued and the static treatment retained.

#### Automation, AI and self-service

- **Shipped an automated surgery consult booking service** combining a pincode-to-nearest-hospital
  API with a full conversational booking flow: ~10 bookings/day with no human involvement and 60–70
  surgeries/month, equivalent to 5–6 agents of capacity at 11–12 surgeries per agent per month.
  Specification to production in under three months.
- **Currently piloting an AI lead-qualification model** scoring intent 0–10, designed to qualify the
  same ~6,000 leads/month with 60% of current agent headcount. Projected distribution: 15% above 7,
  50% between 4 and 7, 35% below 4 — routing high-intent leads to agents and the rest to automation.
- **Built the organisation's first CRM chatbot** with no internal precedent and no vendor playbook.
  It became the foundation the auto-booking service was built on.

#### Retention, feedback and closing the data loop

- **Closed a broken post-surgery data loop.** Once a patient submitted a form their record moved into
  the CRM and left the MediBuddy ecosystem, so completed surgeries never flowed back to the app.
  I specified a discharge order surfacing bills, invoices, discharge summaries and prescriptions
  in-app across 3,300+ surgeries — restoring the round trip and giving the patient a reason to return.
- **Built the voice-of-customer loop**, capturing CSAT and NPS through Typeform and the CRM across
  surgery and dental — sustaining **CSAT above 60 and NPS above 7** — and rebuilt the WhatsApp
  response journey so both lines reported into separate buckets, raising attendance capture 3–4%.
  Designed the underlying lifecycle layer of 22 email and 14 WhatsApp touchpoints mapped to funnel
  stage.

#### Organic growth and market analysis

- **Built the demand model behind the organic growth programme**: a 50-city × 36-procedure map
  covering 229,799 surgeries and 750 city-condition pairs, an audit of 3,231 site URLs and ~23,300
  competitor keywords across three competitors, and a quarter-over-quarter Search Console comparison
  across 1,000 queries and pages. Estimated impact: 5,000 leads/month.
- **Identified an unquantified technical blocker** — mobile performance scores of 33–43 and mobile
  LCP of 10.8–16.9 seconds on the pages the programme depended on — and proposed the URL
  architecture and master content template for cost-comparison pages.

#### Platform and data foundations

- **[Owned the customer side of a full CRM replacement across ~350 seats](./case-studies/crm-migration.md)**
  (LeadSquared → SuperLeap), retiring two systems and cutting over a live operation carrying ~5,000
  outbound calls/day with no business interruption. Owned data preparation, cleaning and validation
  across 300+ GB and 76,903 records — explicitly excluded from the vendor contract — and identified
  two lines of business missing from the vendor requirements document before build.
- **Built the previous CRM from an unstructured instance into the operating system of the business**:
  250+ data points, trigger logic, task and follow-up rules, ownership routing, 62+ automation
  workflows and 5 internal tools. Improved funnel data integrity: duplicate-lead protection 180 →
  290/day, reverse duplicates 20% → 15%, inbound call connect rate 1-in-10 → 5-in-10.
- **Owned the data and reconciliation layer of a nationwide corporate vaccination programme**
  delivered by field teams: 1,340 camps, 175 corporate accounts, 104 cities, 117 hospital partners,
  249,000 doses against ₹27.9 Cr of billing. Built the three-way reconciliation run before every
  invoice; **308 of 838 dual-source camps disagreed, and resolving 7,666 doses of variance protected
  ~₹72 lakh in billing accuracy.**

### Zingbus — Gurugram
**Associate Program Manager, South Zone** · May 2022 – Jul 2022

- **Designed and launched 10 intercity routes for the South India zone** — Bangalore to Hyderabad,
  Mysore, Mangalore, Goa, Shimoga, Bellary and Tirupati among them — defining city pairs, service
  frequency and time-of-day scheduling from competitive market and schedule analysis mapped against
  demand by corridor. Delivered a running timetable within a fixed three-month engagement.

### OLX People — Gurugram
**Operations Manager** · May 2019 – Mar 2021

- Scaled supply for high-volume hiring **12×** while cutting turnaround time **3×** across 10+ new
  cities; improved conversion-to-joining **10% → 17%** and self-applied candidate share
  **15% → 25%**.
- Led a 30-person team across 5 accounts billing more than ₹20 lakh/month.

---

## Shipped and public

| | |
|---|---|
| [Cashless Hospital Finder](https://www.medibuddy.in/surgery-care/find-hospitals) | Live in production · ~50 leads/day · ₹21 lakh/month |
| [Policy Decoder](https://www.medibuddy.in/surgery-care/policy) | Live in the MediBuddy app *(signed-in users)* · [public prototype](https://raopunit95.github.io/gmc-decoder/) |
| [Surgery Network Finder](https://github.com/raopunit95/surgery-network-finder) | Open-source prototype behind the hospital finder · [demo](https://raopunit95.github.io/surgery-network-finder/) |
| [GMC Decoder](https://github.com/raopunit95/gmc-decoder) | Open-source prototype behind the Policy Decoder |

---

## Education

**Sardar Vallabhbhai National Institute of Technology (NIT), Surat**
Integrated M.Sc., Applied Mathematics · 2014–2019 · CGPA 8.21

---

## Skills

**Product** — discovery & user research · PRDs · phased scoping & effort estimation · roadmapping ·
A/B testing & experiment design · funnel and journey design · catalog and taxonomy design ·
payments, deposits, refunds and cancellation policy · lifecycle CRM · cross-sell · GTM

**Analytics** — SQL (MySQL) · CleverTap · Hotjar · Google Analytics via Google Tag Manager ·
Snowplow · Apache Superset · Looker Studio · Redash · PromptQL · Search Console · Python (working)

**Platforms** — LeadSquared · SuperLeap · Retool · Typeform · n8n · REST APIs · Webhooks ·
WhatsApp Business API · cloud telephony · Jira · Confluence · Figma

**Domain** — digital health · corporate group health insurance (GMC) · elective surgery · dental ·
provider networks · claims · intercity mobility

---

## Languages
English · Hindi
