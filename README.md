# Punit Yadav — Product Manager

I own the acquisition-to-surgery funnel at [MediBuddy](https://www.medibuddy.in) — the journey a
patient takes from a symptom search to a booked, insured, completed procedure. That line runs
~1,500 procedures and ~₹11 Cr a month, and grew ₹100 Cr → ₹130 Cr → ₹150 Cr while I owned its
demand side.

Seven years in, five of them in digital health. Applied Mathematics at NIT Surat. I write SQL,
instrument my own events, and build the prototype myself when that's the fastest way to find out
whether an idea deserves a sprint.

📍 Gurugram, India · ✉️ puneetyadav95@gmail.com · [LinkedIn](https://linkedin.com/in/punit-yadav-2ab6a013b) · 🌐 [Portfolio site](https://raopunit95.github.io/punit-yadav/)

---

## Case studies

Write-ups with the reasoning left in — the options I rejected, the things I chose *not* to build,
and the results.

### 🏥 [Cashless Hospital Finder — live in production](./case-studies/hospital-finder.md)
**[▶ Live](https://www.medibuddy.in/surgery-care/find-hospitals)** · [prototype demo](https://raopunit95.github.io/surgery-network-finder/) · [source](https://github.com/raopunit95/surgery-network-finder)

A patient wants one answer: *where can I have this surgery done, near me, cashless on my insurance?*
Insurer lists are PDFs by city, hospital directories are filed by department, and neither is
organised the way anyone asks — so the lead form standing in for an answer lost 80% of its users.
Replaced it with pincode or city plus treatment and insurer, returning hospitals ranked by distance,
rating and insurance panel, then the doctors there who perform that procedure. I built the prototype
myself to prove the condition-to-speciality matching before committing a sprint.
**~50 leads/day · ~30 surgeries/month · ₹21 lakh of booked value monthly**

### 🔓 [Policy Decoder — insurance transparency as a growth lever](./case-studies/policy-decoder.md)
**[▶ Live in the app](https://www.medibuddy.in/surgery-care/policy)** *(signed-in users)* · [public prototype](https://raopunit95.github.io/gmc-decoder/) · [source](https://github.com/raopunit95/gmc-decoder)

Patients defer elective surgery when they can't tell what their corporate policy covers. I built the
prototype myself to test whether resolving that changed behaviour, then owned the PRD for the
production feature — including the access-control model that keeps one employer's policy data from
leaking to another.
**~2,300 leads/month across all entry points · live for 19 corporate accounts × 90+ conditions**

### 🦷 [Dental Procedure Booking — a deposit-and-settlement flow](./case-studies/dental-booking.md)
Turning dormant corporate wallet balances into booked procedures. 22 requirements phased into an
18-item V0 at ~41 person-days: a 470-SKU catalog, a ₹499 deposit with post-procedure settlement,
cancellation and refund rails, and an operations settlement dashboard.
**₹16–17 Cr/yr run rate → ₹27 Cr target (+75%) · one 7-day build removed from scope**

### 📱 [New Services hub — winning a slot in the bottom nav](./case-studies/bottom-nav-hub.md)
Prime app real estate is zero-sum: five icons, no sixth. I used tap data across ~1.5M monthly
interactions to prove which icon should lose its place.
**~180k unique users/month · ~10,000 surgery landings → ~4,000 leads at a 40% landing-to-lead rate**

### 🔄 [CRM replacement — 350 seats, two systems retired, zero downtime](./case-studies/crm-migration.md)
Owned the customer side of a full CRM migration on a live operation carrying ~5,000 outbound calls
a day — data model, integrations, and the data cleansing the vendor contract explicitly excluded.
**300+ GB and 76,903 records migrated · document pipeline 11,400 → 37,700 records/hour**

---

## How I work

**Discovery before sizing.** The Policy Decoder exists because of a sentence that kept coming up in
user conversations — *"I don't know what my company's policy covers"* — that no dashboard would
have surfaced.

**Smallest thing that produces a real signal.** A no-code CMS beat a proper CMS build by a quarter.
A self-built prototype beat waiting for a sprint slot — twice, and both are in production now.
Cutting a rule engine down to a single eligibility check saved seven engineering days and lost nothing.

**Say no in writing.** Every deferral in my specs carries a reason. The decisions-made and
questions-open register is the part of a PRD I care most about.

**Instrument before launch.** I build the dashboards, so I don't ship what I can't read.

---

## Selected numbers

| | |
|---|---|
| Cashless Hospital Finder | ~50 leads/day → ~30 surgeries/month → ₹21 lakh booked value/month |
| Funnel entries | 90k → 150k/month (1.4× leads at flat acquisition cost) |
| Insurance transparency | ~2,300 leads/month |
| Bottom-nav hub | ~4,000 leads/month from ~10,000 landings |
| Automated booking | ~10 bookings/day, 60–70 surgeries/month, no human in the loop |
| Condition pages | conversion 1.2% → 1.4% |
| CRM migration | ~350 seats, 300+ GB, zero downtime |
| Billing reconciliation | ~₹72 lakh of variance resolved across a ₹27.9 Cr programme |
| Satisfaction | CSAT > 60, NPS > 7 |

---

## What I work with

| | |
|---|---|
| **Product** | Discovery & user research · PRDs · phased scoping & effort estimation · roadmapping · A/B testing · funnel & journey design · catalog and taxonomy design · payments, refunds & cancellation policy · GTM |
| **Analytics** | SQL (MySQL) · CleverTap · Hotjar · Google Analytics via GTM · Snowplow · Apache Superset · Looker Studio · Redash · PromptQL · Search Console |
| **Platforms** | LeadSquared · SuperLeap · Retool · Typeform · n8n · REST APIs · Webhooks · WhatsApp Business API · Jira · Confluence · Figma |
| **Domain** | Digital health · corporate group health insurance (GMC) · elective surgery · dental · provider networks · claims |

---

## Built in public

| Repository | What it is |
|---|---|
| [surgery-network-finder](https://github.com/raopunit95/surgery-network-finder) | The prototype behind the Cashless Hospital Finder. 648 hospitals, 3,547 doctors, 218 surgeries. Static site, zero dependencies. [Demo](https://raopunit95.github.io/surgery-network-finder/) |
| [gmc-decoder](https://github.com/raopunit95/gmc-decoder) | The prototype behind the Policy Decoder. 19 corporates, 208 conditions, 7,072 coverage rules. [Demo](https://raopunit95.github.io/gmc-decoder/) |

---

## More

🌐 [Portfolio site](https://raopunit95.github.io/punit-yadav/) · 📄 [Full resume](./resume.md) · [PDF](./resume.pdf) · 🤖 [profile.json](./profile.json) *(machine-readable)*

---

**Open to Product Manager roles** in consumer platforms, marketplaces, health tech and travel —
Gurugram/NCR, Bengaluru or remote. **puneetyadav95@gmail.com**
