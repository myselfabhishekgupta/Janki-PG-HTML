# Janki PG — Website Plan

Girls Paying Guest (PG) accommodation website — project proposal and requirements.

**Prepared for:** Janki PG (Girls Paying Guest Accommodation)
**Date:** July 2026

---

## Overview

This repository contains the website for **Janki PG**, a Girls Paying Guest accommodation. This document explains the website in plain language — what will be built, what we recommend leaving out for now, and exactly what information is needed before work can begin.

Two very different people visit this website, and the site is built around both of them:

- **The student** wants to know: What do the rooms look like? Is the WiFi good? How is the food? What does it cost?
- **The parent** wants to know: Is she safe there? Is it clean? Are there rules? Who is watching the gate at night?

The parent is usually the one who pays and gives final approval. So the website is designed to reassure the parent first, and impress the student second. Every decision below comes back to that.

---

## 1. Pages

| Page | What it does |
|---|---|
| **Home** | First impression. Large photo, welcome message, and four clear buttons: Book Now, Enquire, WhatsApp, Call. Below that, a summary of the best reasons to choose Janki PG. |
| **About Us** | Story, standards, and why students stay. Where trust is built. |
| **Rooms & Pricing** | The most important page. All six room options with prices for monthly, quarterly, half-yearly, and yearly stays. |
| **Amenities** | All facilities shown as easy-to-scan cards with icons — AC, WiFi, food, CCTV, geyser, laundry and so on. |
| **Gallery** | Photographs of the building, rooms, dining area, kitchen, washrooms and food. Click-to-expand lightbox. |
| **Enquiry** | Form asking for name, phone, city, college, room preference and move-in date. Every submission arrives by email instantly. |
| **Contact** | Phone, WhatsApp, address, business hours, and a Google Map with a "Get Directions" button. |
| **House Rules & Safety** | Visitor policy, gate timings, security arrangements, emergency contact. Parents look for exactly this. |
| **Privacy Policy / Terms** | Standard legal pages every website needs. |

---

## 2. Pricing logic

Base monthly rates:

| Room type | Single sharing | Double sharing | Triple sharing |
|---|---|---|---|
| A/C rooms | ₹20,000 | ₹12,000 | ₹9,000 |
| Non-A/C rooms | ₹17,000 | ₹9,000 | ₹7,000 |

The pricing section has a duration switcher — **Monthly · Quarterly · Half-Yearly · Yearly** — that updates every price on the page instantly. Longer durations are calculated from the monthly rate (quarterly = monthly × 3, and so on).

### Open decision: long-stay discount

At present, a yearly booking costs exactly twelve times the monthly rate, giving no financial incentive to commit long-term. A standard ~5% long-stay discount would look like this for an A/C double-sharing room:

- Twelve months at full price: **₹1,44,000**
- With a 5% discount: **₹1,36,800** — a saving of ₹7,200

This needs a decision from the client before the pricing page is finalised — whether to apply a discount, and at what rate.

### Terms displayed on the pricing page

- Electricity charged separately for A/C rooms, based on actual usage
- Electricity included in rent for Non-A/C rooms
- One month security deposit
- One month advance rent
- One month notice period before vacating

---

## 3. WhatsApp integration

All WhatsApp buttons use click-to-chat with a **pre-filled message** based on context. Example — tapping WhatsApp from the A/C double-sharing price card opens:

> "Hi, I'm interested in Janki PG. Room: A/C Double Sharing"

A floating WhatsApp button is present on every page.

**Note:** the WhatsApp Business API is not used — it requires Meta business verification, a paid third-party provider, and per-conversation charges, and is built for high-volume automated messaging. Click-to-chat achieves the same outcome at no cost.

---

## 4. Deferred for v1

| Feature | Reason |
|---|---|
| Dark mode | Wrong tone for this category — parents respond to bright, clean, airy. Doubles design/testing effort for minimal benefit. |
| 360° virtual tour | Requires specialist camera equipment and a paid hosting service. Photos suffice for launch. |
| Live "Check Room Availability" | Requires constant manual updates or it actively damages trust. Replaced with "Enquire about availability" → WhatsApp. |
| Automatic Google Reviews feed | Requires a paid Google API integration. Static testimonials + link to Google listing instead. |
| Video walkthrough | Space reserved in layout; add once footage is available. |

---

## 5. Google Business Profile

The website is roughly 30% of discoverability; the Google Business Profile listing is the other 70%. This should be treated as part of the project scope, not optional:

- Claim and verify the Janki PG listing on Google
- Set category to "Women's hostel"
- Upload the same photography used on the site
- Request reviews from current/departing residents

---

## 6. Information required

### Blocking (needed before launch)

1. Full address + Google Maps location
2. Business email address (for enquiry form delivery)
3. 15–20 real photographs — exterior, entrance, all room types, dining, kitchen, washroom, common area, food
4. Meal details — veg/non-veg, timings
5. Visitor policy and gate timings
6. Logo (or budget for one to be designed)

> **On photographs:** use real, phone-quality photos of the actual property — not stock imagery. Prospective residents and parents are comparing multiple PGs and can tell immediately when a photo isn't the real building. Authentic imperfection outperforms polished stock photos here.

### Non-blocking (can follow post-launch)

7. Nearby colleges, coaching institutes, offices, hospitals, bus stops (with distances)
8. Instagram / Facebook links
9. Google Reviews link
10. Laundry charges (if applicable)
11. Parking availability
12. Cancellation and refund policy
13. UPI / Razorpay integration (phase 2)

---

## 7. Timeline

~6 working days from receipt of blocking items above.

| Day | Work |
|---|---|
| 1 | Project setup, colours, fonts, header/footer |
| 2 | Home page |
| 3 | Rooms & Pricing page, including duration switcher |
| 4 | Amenities, Gallery, FAQ |
| 5 | Enquiry form, Contact page, legal pages |
| 6 | SEO/Google optimisation, performance testing, mobile QA |

---

## 8. Deliverables

- Full multi-page website per the structure above
- Responsive across mobile, tablet, desktop
- Fast-loading, optimized assets
- SEO-configured (indexable, structured data, sitemap)
- Working enquiry form with email delivery
- WhatsApp + click-to-call integration throughout
- Accessible design (WCAG-friendly)
- Deployed and live, with a maintenance plan

---

## 9. Open questions for the client

1. Discount for quarterly / half-yearly / yearly bookings — apply, and at what rate?
2. Is laundry included, charged separately, or not offered?
3. Is parking available for residents or visitors?
4. Check-in / check-out timings?
5. Preferred domain name (e.g. `jankipg.com`)?
6. Existing brand colours, or should a palette be proposed?

---

## Tech stack

- **Framework:** Astro + Tailwind CSS
- **Forms:** Web3Forms
- **Images:** `astro:assets` for automatic optimization
- **Hosting:** Netlify / Vercel

---

*Work begins once the blocking items in Section 6 and answers to Section 9 are received.*