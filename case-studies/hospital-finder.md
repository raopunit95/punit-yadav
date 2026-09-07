# Cashless Hospital Finder

**A translation problem wearing a search box — and why the department is not a matching key**

🔗 **[Live in production](https://www.medibuddy.in/surgery-care/find-hospitals)** ·
[Prototype demo](https://raopunit95.github.io/surgery-network-finder/) ·
[Prototype source](https://github.com/raopunit95/surgery-network-finder)

Role: PM (owner) — discovery, prototype, PRD, launch · ~50 leads/day → ~30 surgeries/month → ₹21 lakh/month

---

## Context

MediBuddy's surgery line runs ~1,500 elective procedures and ~₹11 Cr a month, 95% of it through
corporate group medical cover. I own the acquisition funnel feeding it.

A patient who has decided to have surgery asks one question before anything else:

> *"Where can I have this done, near me, without paying upfront?"*

Every part of that answer existed in our systems. None of it was reachable in the words the patient
would use. The surface standing in for an answer was a lead-capture form — name, phone, condition,
submit, wait for a callback — and **it was losing 80% of the people who reached it.**

## Problem

Three things have to be true at once for a hospital to be the right answer: it does the procedure,
it's on the patient's insurer panel, and it's close enough to travel to. Today a patient
cross-references those three by hand, from sources organised along none of them:

- **Insurer network lists** are PDFs organised by city.
- **Hospital directories** are organised by medical department.
- **Nothing at all** tells you whether a surgeon who performs that procedure actually sits there.

Underneath the UX problem was a vocabulary problem, and it turned out to be the real one. **Patients
describe a condition or a procedure. The provider network is filed by department.** Someone types
*Piles*; the inventory says *General Surgery*. Search the network for the word the patient used and
you get nothing back — not because no hospital treats it, but because the word appears nowhere in
the data.

A lead form is what you build when you can't answer the question. It converts the patient's intent
into a callback queue and spends a coordinator's time reconstructing, by phone, something the data
already knew.

## Options I considered

| Option | Why I didn't pick it |
|---|---|
| Add fields to the existing lead form | Treats the symptom. The form wasn't failing because it was short — it was failing because it gave nothing back. |
| Static city-wise cashless hospital pages | Answers location, ignores procedure and insurer. Also unmaintainable: 144 cities × 36 insurers. |
| Real-time network API integration per insurer | The correct long-term answer, and multiple quarters of engineering plus partnership dependencies. Far too slow to test whether patients would use this at all. |
| Let the CRM route it — better lead qualification | Optimises the callback, keeps the patient waiting. The whole point was to answer without a human in the loop. |
| **Structured network snapshot + client-side finder** ← chose this | Testable in weeks against data we already hold. If nobody used it, we'd have lost weeks rather than quarters. |

**What I explicitly chose not to build:** real-time bed availability, in-flow appointment booking,
cost estimation, and doctor ratings. All were asked for. None of them tested the actual question —
*does answering "where, cashless, near me" convert intent that a form was losing?*

## What I shipped

**v1 — the prototype, built by me.** Before asking for a sprint, I built a working version to prove
the two things I wasn't sure about: that ranking by distance would produce sensible answers across a
country-sized network, and that the condition-to-department mapping could be made to work at all.

Plain HTML, CSS and JavaScript over generated JSON. No backend, no framework, no dependencies. It
covers **648 hospitals, 3,547 doctors, 218 surgeries, 144 cities and 36 insurers**, and three
decisions in it survived into production:

**The department is a filing category, not a matching key.** Routing a surgery to hospitals through
its department works for departments that map to a single speciality and fails badly for the
catch-alls. `Aesthetic` spans plastic surgery, dermatology, cosmetology and hair transplants — so
routed naively, *Rhinoplasty* matched hair clinics and *Botox* matched surgical wards. `General
Medicine` spans eight specialities including General Surgery, so *Dengue* returned surgical
hospitals. The fix is an override: a surgery may skip its department and name the specialities it
actually needs. 45 of the 218 do; the rest use the department route, which is correct for them.

**Distance sets the shortlist; quality decides within it.** Sorting the whole result set by rating
put a 4.9 in Vizianagaram above a 4.6 in Noida for a patient searching from Rajasthan —
arithmetically correct, useless as an answer. Results are grouped into distance bands, bands are
always nearest-first, and no sort can move a hospital out of its band. Inside a band the default
order weighs admission volume and review-adjusted rating, because for surgery a busy hospital 8 km
away beats a quiet one 3 km away.

**"Nothing nearby" is an answer, not an error.** Pincode 333515 (Jhunjhunu) has no
knee-replacement hospital within 50 km; the nearest is 109.5 km away in Gurgaon. Showing an empty
screen tells the patient no option exists, which is false. Showing Gurgaon in a normal-looking list
hides the distance until they're invested. The page widens the search and says so, with the real
number, before the first hospital name.

**v1.1 — the production feature.** GPS, pincode or city, plus treatment and insurer, returning
hospitals ranked by distance, rating and insurance panel — then the doctors at the chosen hospital
who perform that specific procedure, separated from the rest of the roster. The mapping layer behind
it standardises 218 sub-departments across 24 departments, and the same layer drives site search and
CRM opportunity routing.

## Result

| | |
|---|---|
| Leads | ~50 / day |
| Surgeries booked | ~30 / month |
| Booked value | **₹21 lakh / month** (~₹2.5 Cr annualised) |
| Target set | Form completion 19% → 45% |

**On attribution, honestly:** these are leads originating on the finder surface measured against the
pre-launch baseline for the form it replaced — not a holdout. Some share of those patients would
have reached us through another entry point eventually. The booked value is attributed on
first-touch, which flatters any top-of-funnel surface, this one included.

## What I'd do differently

- **Run a holdout.** Same self-inflicted problem as the Policy Decoder. The number is big enough to
  be worth defending properly.
- **Fix the source data instead of reporting it.** Around two dozen hospitals have a blank insurer
  field, usually because the whole panel was pasted into one cell without commas. Those hospitals
  vanish the instant a patient selects an insurer. I built tooling that names them on every refresh;
  I did not get them corrected at source, which is the only fix that lasts.
- **37 mappings are still unreviewed.** Surgeries under Gynaecology and Oncology match more than
  three specialities each. Defensible — a cancer patient plausibly wants any oncology unit — but
  "defensible" is not "reviewed", and I left it that way.
- **Treat the map links as perishable.** A fifth of the hospital records point at `goo.gl` short
  links, and that shortener is being retired. A rotted link still looks valid until someone taps it.
- **Show the roster gap earlier.** Some hospitals are on the panel with no individual surgeon
  listed. The page says so honestly, but I found that out from the data rather than from the ops
  team, and they'd have told me on day one.

---

**Demonstrates:** funnel-leak diagnosis → taxonomy and information architecture design → prototyping
to de-risk a spec → ranking design under a real-world constraint → honest handling of absent data →
measured launch.
