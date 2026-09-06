# New Services Hub

**Winning a slot in the bottom navigation — a zero-sum negotiation settled with data**

Role: PM (owner) — analysis, PRD, launch · Platforms: Android and iOS

---

## Context

I own the surgery acquisition funnel. Surgery is a high-value, low-frequency service on an app whose
daily habits are built around high-frequency ones — benefits, reorders, family profiles. The
structural problem: **people don't open a health app looking for surgery.** They open it for
something else and discover surgery only if it's in their path.

The app's bottom navigation is the most valuable real estate on the product. It also holds exactly
five icons and cannot hold six.

## Problem

Asking for a bottom-nav slot means asking another team to give one up. That's not a design argument,
it's a political one — and political arguments are won with evidence or not at all.

So I pulled tap data across the bottom navigation: **~1.5M monthly taps** in total. The distribution
was not close.

| Bottom-nav destination | Monthly taps |
|---|---|
| Benefits | 678,661 |
| Reorder | 499,922 |
| Family | 402,812 |
| MediMaps | **807** |
| **Total** | **1,582,202** |

**MediMaps held 0.05% of the traffic** — roughly one tap in every two thousand — while occupying a
fifth of the most valuable surface in the product. That single row settled a discussion that
opinion alone would not have.

## Options I considered

| Option | Why I didn't pick it |
|---|---|
| Add a sixth icon | Platform constraint: five is the maximum. Not available. |
| Put surgery directly in the vacated slot | Wasteful. One low-frequency service would inherit prime real estate it can't fill on its own, and every other new service would have to fight the same battle again next quarter. |
| Banner or carousel on the home screen | Already tried across the product; carousel positions past the first are close to invisible, and it doesn't survive a home-screen redesign. |
| **A "New Services" intermediate hub in the vacated slot** ← chose this | One slot serves Surgery, Wellness, Programs and Fitness. It amortises a scarce resource across four services instead of one, so the next launch inherits distribution instead of re-fighting for it. |

Choosing the hub over the direct link was the actual product decision. It gave me less surgery
traffic than a dedicated icon would have, and made the change defensible to every other service
owner — which is why it shipped at all.

## What I shipped

An intermediate hub page reached from the bottom navigation, listing service categories as cards
that deep-link into their destinations.

Specified in the PRD:

- **Entity-level configuration** — the tab can be enabled or disabled per corporate entity, so a
  client without a service never sees a dead end.
- **A "New" tag** on the tab, togglable, to drive first-time discovery without a permanent badge.
- **Deep-link fallback** — any broken or unavailable deep link returns the user to the home screen
  rather than a blank state. Cheap to specify, and the difference between a bad day and a crash
  report.
- **Back-navigation behaviour** — returning from a service goes back to the hub, not the home
  screen, so browsing several services doesn't require starting over.
- **Snowplow event tracking** on every interaction, capturing platform, timestamp, user and entity
  identifiers, source, screen and item name — so the value of each card could be measured
  independently rather than argued about later.
- **Android and iOS first**, web deferred to a later phase.

## Result

| | |
|---|---|
| Hub reach | ~180k unique users/month · ~10k unique visitors/day |
| Surgery landings | ~300/day · **~10,000/month** |
| Surgery leads | **~4,000/month** |
| Landing-to-lead conversion | **~40%** |

Surgery captures roughly 3% of daily hub traffic. That sounds small until you look at the second
number: **four in ten people who land on the surgery page from this hub become a lead.** Intent
routed from inside the product converts at a rate paid traffic does not come close to — which is the
whole argument for spending scarce navigation real estate rather than media budget.

It is now the single largest entry point into the surgery funnel.

## What I'd do differently

- **Instrument the hub page itself, not just the destinations.** I can see who arrives at surgery.
  I have a much weaker view of who opened the hub, scanned four cards and chose nothing — and that
  cohort is the one that tells me whether the card copy is doing its job.
- **A/B the card order and labels.** They shipped as a considered guess and have never been tested.
  With ~10k daily visitors the experiment would reach significance in days.
- **Define shared success metrics with the other three services up front.** I built the case, so the
  measurement got built around surgery. A hub owned by four teams needs a scorecard all four
  recognise, or it quietly becomes a surgery feature that three other services are tenants of.
- **Say more clearly what happens to MediMaps users.** 807 taps is a small number of people, but it
  isn't zero, and the spec should have named their alternative path rather than leaving it implied.

---

**Demonstrates:** using usage data to win a zero-sum resource negotiation · designing for reuse over
local optimisation · specifying failure states and configurability · instrumentation as an argument
you make before the launch, not after.
