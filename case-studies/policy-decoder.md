# Policy Decoder

**Insurance transparency as a growth lever — and the access-control problem underneath it**

🔗 **[Try the live prototype](https://raopunit95.github.io/gmc-decoder/)** ·
[Prototype source](https://github.com/raopunit95/gmc-decoder) ·
[Production feature](https://www.medibuddy.in/surgery-care/policy)

Role: PM (owner) — discovery, prototype, PRD, launch · Live for 19 corporate accounts × 90+ conditions

---

## Context

MediBuddy's surgery line runs ~1,500 elective procedures and ~₹11 Cr a month. **95% of that demand
comes through corporate group medical cover (GMC)** — the procedure is, in principle, already paid
for by the patient's employer policy.

I own the organic acquisition funnel feeding it. The largest single leak in that funnel sat between
lead and consult: people who had raised their hand and then stopped.

## Problem

Dashboards told me *where* people stopped. They couldn't tell me why. So I ran conversations with
dropped-off leads, and the same sentence kept coming back in different words:

> *"I don't know what my company's policy actually covers."*

The mechanic underneath it: a patient facing elective surgery will not commit to a consult while the
financial outcome is unknown. Copay, room-rent caps, waiting periods and procedure sub-limits vary
by employer **and by grade within the same employer**, and the policy document is forty pages of
legalese the employee has never opened.

**People weren't saying no. They were saying not yet** — and not-yet is where the funnel dies
silently, because it never shows up as a rejection.

## Options I considered

| Option | Why I didn't pick it |
|---|---|
| Train coordinators to explain coverage on the call | Only helps *after* the lead talks to a human — but the drop happens before that. Also adds handle time to a team already at capacity. |
| A static "understand your GMC" content page | Generic content can't answer *"what does **my** policy cover"*. The specificity is the entire value. |
| Real-time eligibility integration with each insurer | The correct long-term answer. Multiple quarters of engineering and a set of partnership dependencies — far too slow to test the hypothesis. |
| **Structured policy dataset + client-side decoder** ← chose this | Tests demand in weeks, no backend, no insurer dependency. If nobody used it we'd have lost two weeks instead of two quarters. |

**What I explicitly chose not to build:** claim-status tracking, policy document upload with OCR, and
personalised total-cost estimates. All were asked for. None of them tested the actual question —
*does removing coverage uncertainty change booking behaviour?*

## What I shipped

**v1 — the prototype, built by me.** Plain HTML, CSS and JavaScript over a structured JSON dataset.
No backend, no framework, no build step. Three inputs: employer, plan grade, condition. One output:
covered amount, room-rent cap, copay, pre- and post-hospitalisation window, inclusions, exclusions
and remarks — in the language a person actually uses.

The current dataset holds **19 corporates, 34 plan grades, 208 conditions and 7,072 coverage rules**
compiled from 2,515 source rows. When a condition has no dedicated rule under the selected plan, the
app says so plainly rather than inventing a number — that decision mattered more than any feature.

**v1.1 — the production PRD, and the part that took the most thought.**

Extending this beyond logged-in users created a data-isolation problem that didn't exist in the
prototype. Corporate GMC terms are commercially sensitive: an employee of one company must never be
able to read another company's policy configuration. The spec therefore defines coverage display as
a function of *proven* identity:

- **Logged-in corporate user** — employer resolved from the profile; coverage shown directly.
- **Unauthenticated corporate user** — must pass a **corporate email domain match plus OTP
  verification** before any GMC data is rendered. Domain mismatch is rejected outright.
- **Retail user** — routed to public policy guidance only, because retail policy summaries are
  public documents and carry no isolation risk.
- **No policy data on file** — an honest fallback message, never a guess.

Grade is resolved server-side from the employee record rather than asked for, so a user can't probe
for a better-covered band than their own.

## Result

| | |
|---|---|
| Live coverage | 19 corporate accounts, 90+ conditions each |
| Decoder page | ~30 leads/day |
| All insurance-transparency entry points combined | **~2,300 leads/month** |

The rollout ran in three stages: the first ten corporates, then nine more once grade-level logic
shipped, then surfacing policy verification directly on the app home screen for the highest-volume
accounts — which turned out to be the largest single contributor, because the feature had existed
for months with too little visibility to be found.

**On attribution, honestly:** these are incremental lead volumes measured against the pre-launch
baseline for the same entry points, not a holdout experiment. A holdout would have made the claim
airtight and I'd design one if I ran this again.

## What I'd do differently

- **Run a holdout.** The lift is large enough to be convincing and soft enough to be arguable. That's
  a self-inflicted problem.
- **Instrument before launch, not alongside it.** Some of the early event tracking was retrofitted,
  which cost me clean funnel data for the first cohort.
- **Solve visibility at the same time as the feature.** The home-screen entry point delivered the
  biggest share of leads and could have shipped in week one. I built a good thing and left it
  somewhere people had to go looking for.
- **Own data freshness explicitly.** A structured policy snapshot goes stale the moment an employer
  renews. The refresh cadence and its owner should have been part of v1, not a follow-up.

---

**Demonstrates:** qualitative discovery → opportunity framing → build-vs-defer tradeoffs → shipping a
testable v1 under constraint → multi-tenant access-control design → staged rollout and measurement.
