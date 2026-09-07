# **Projects & Case Studies — Punit Yadav**

This section contains real product work, experiments, workflows, and systems I've built.

---

## **1. Cashless Hospital Finder (MediBuddy) — live in production**

**🔗 Production:** https://www.medibuddy.in/surgery-care/find-hospitals  
**🔧 Open-source prototype:** https://github.com/raopunit95/surgery-network-finder  
**▶ Prototype demo:** https://raopunit95.github.io/surgery-network-finder/

**Problem.** A patient who needs surgery wants one answer: *where can I have this done, near me,
cashless on my insurance?* Insurer network lists are PDFs organised by city. Hospital directories
are organised by medical department. Neither is organised by the thing the patient actually types.
The existing lead-capture form was losing 80% of the users who reached it.

**What I built.** An interactive finder — GPS, pincode or city, plus treatment and insurer —
returning hospitals ranked by distance, rating and insurance panel, then the doctors at the chosen
hospital who perform that specific procedure.

**Live results**

| Metric | Value |
|---|---|
| Leads | ~50 / day |
| Surgeries booked | ~30 / month |
| Booked value | ₹21 lakh / month (₹2.1M) |
| Target set | Form completion 19% → 45% |

**The interesting problem.** Patients search for a *condition*; hospitals are filed by *department*.
Someone types "Piles", the network says "General Surgery", and nothing connects the two. Solving it
meant building a mapping layer — 218 sub-departments across 24 departments — and discovering that a
department is a filing category, not a matching key: the catch-all department "Aesthetic" covers
plastic surgery, dermatology, cosmetology and hair transplants, so routed naively, a nose job
matched hair clinics.

**How it was de-risked.** I built the working prototype myself and published it, to prove the
distance ranking and the condition-to-speciality matching before asking for an engineering sprint.
The prototype covers 648 hospitals, 3,547 doctors, 218 surgeries, 144 cities and 36 insurers as a
static site with zero dependencies.

---

## **2. Surgery Booking Chatbot (MediBuddy)**
- Automated OPD bookings through WhatsApp/Typeform  
- Saved 6 FTE operational load  
- Generated ₹35L/month revenue by auto-bookings  

---

## **3. LeadSquared CRM Implementation**
- Customised CRM from scratch as per the business need.  
- Created design that managed ~100k monthly leads.
- Created 62+ automations, communications, alerts for insurance, ops, marketing, and product  

---

## **4. COVID Vaccination Program Analytics**
- Built 200+ charts for real-time monitoring  
- Tracked 2.2L vaccination shots across India  

---

## **5. Hospital Locator System**
- Mapped 1200+ hospitals & 8700+ doctors  
- Used pincode-based routing logic  
- Powered OPD & Surgery discovery features  
- Became the foundation for the Cashless Hospital Finder above, which added insurer matching,
  distance-banded ranking and doctor-level results on top of the same locator idea

---

## **6. GMC Policy Decoder**
- Corporate health policies are 40 pages of legalese; that uncertainty was stopping people booking surgery  
- Three taps, one answer: what your plan covers for your condition  
- 19 corporates, 208 conditions, 7,072 coverage rules  
- **[Live demo](https://raopunit95.github.io/gmc-decoder/)** · **[Source](https://github.com/raopunit95/gmc-decoder)** · [Case study](./case-studies/policy-decoder.md)  

---

More case studies coming soon.

---
