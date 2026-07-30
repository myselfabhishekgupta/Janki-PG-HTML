# CLAUDE.md — Janki PG Website

This file gives Claude Code the full context for this project. Read it fully before writing any code. Work page by page, not all at once — see "How to work" at the bottom.

---

## 1. Project summary

Janki PG is a Girls Paying Guest (PG) accommodation. This repo is its marketing/booking website: a multi-page, SEO-friendly, mobile-first site whose job is to convert visitors into WhatsApp messages, calls, or enquiry form submissions.

There are two audiences, and both must be satisfied on every page:

- **Students** — care about rooms, WiFi, food, price.
- **Parents** — care about safety, hygiene, rules, supervision. Parents usually make or approve the final decision, so **design for the parent first, the student second.** Safety and trust signals (CCTV, female-only staff, hygiene, rules) should never feel buried.

Full requirements and rationale live in `README.md` in this repo — read it before starting. This file (`CLAUDE.md`) is the technical/build instruction; `README.md` is the plain-language project plan.

---

## 2. Tech stack

- **Framework:** Astro (latest stable) — static output, islands only where truly interactive
- **Styling:** Tailwind CSS — utility-first, no separate CSS files unless global
- **Forms:** Web3Forms (enquiry form submission, no backend needed)
- **Images:** `astro:assets` (`<Image />`) for all photos — automatic WebP/AVIF, explicit width/height, lazy loading by default
- **Icons:** `astro-icon` + Lucide icon set (inline SVG, no icon fonts)
- **Lightbox:** GLightbox or PhotoSwipe for the gallery — lightweight, no framework dependency
- **Animations:** CSS `@keyframes` + IntersectionObserver for scroll-reveal. Do not add a heavy animation library like AOS or Framer Motion for this project.
- **Sitemap:** `@astrojs/sitemap`
- **Hosting target:** Netlify or Vercel (static build)
- **No dark mode.** Do not build a theme toggle — see README Section 4 for reasoning.

Do not introduce React, Vue, or any UI framework. This site does not need one — Astro components and a handful of `<script>` islands are sufficient for the switcher, accordion, and lightbox.

---

## 3. Design direction

- **Palette:** warm and premium, not corporate. Base: white / soft cream background, deep teal or navy for headings and primary buttons, a warm gold or coral accent for highlights and CTAs. Confirm exact hex values with the client before locking the Tailwind theme — placeholders are fine to start.
- **Typography:** one distinctive heading font (e.g. a serif or rounded display face) + a clean sans-serif for body text. Avoid default system fonts — this should not look like a template.
- **Component language:** rounded cards, soft shadows, generous whitespace. Use glassmorphism sparingly — at most the sticky nav on scroll and one hero panel. Do not apply it broadly; it hurts text contrast and accessibility.
- **Imagery:** real photos only, never stock. Until real photos are supplied, use clearly-labelled placeholder blocks (not fake stock images) so it's obvious what still needs replacing.
- Read `/mnt/skills/public/frontend-design/SKILL.md`-equivalent conventions if available in this environment before styling — favor intentional, non-templated design choices over generic Tailwind defaults.

---

## 4. Project structure

```
janki-pg/
├── public/
│   ├── robots.txt
│   ├── favicon.svg
│   ├── og-image.jpg
│   └── brochure.pdf              # placeholder until client supplies one
├── src/
│   ├── data/
│   │   ├── site.json             # phone, whatsapp, address, hours, socials, email
│   │   ├── pricing.json          # room types + monthly rates + duration multipliers
│   │   ├── amenities.json
│   │   ├── testimonials.json
│   │   ├── faqs.json
│   │   └── nearby.json
│   ├── components/
│   │   ├── layout/                → Header, Footer, Nav, MobileMenu
│   │   ├── ui/                    → Button, Card, SectionHeading, Badge
│   │   ├── home/                  → Hero, WhyChooseUs, PricingPreview, AmenitiesPreview, TestimonialSlider, CtaBand
│   │   ├── PricingTable.astro     # duration switcher lives here
│   │   ├── AmenityGrid.astro
│   │   ├── Gallery.astro
│   │   ├── FaqAccordion.astro     # native <details>/<summary>, no JS needed
│   │   ├── EnquiryForm.astro
│   │   ├── FloatingActions.astro  # WhatsApp + Call + Back-to-top
│   │   └── seo/                   → BaseHead.astro, LodgingSchema.astro
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro
│   │   ├── about.astro
│   │   ├── rooms-and-pricing.astro
│   │   ├── amenities.astro
│   │   ├── gallery.astro
│   │   ├── enquiry.astro
│   │   ├── contact.astro
│   │   ├── house-rules.astro
│   │   ├── privacy-policy.astro
│   │   └── terms.astro
│   └── styles/global.css
├── astro.config.mjs
├── tailwind.config.mjs
└── package.json
```

---

## 5. Data model — read this before building the pricing page

All prices are derived from six base monthly rates. Never hardcode a duration price anywhere — compute it.

```json
// src/data/pricing.json
{
  "durations": [
    { "id": "monthly",  "label": "Monthly",       "months": 1  },
    { "id": "quarterly","label": "Quarterly",     "months": 3  },
    { "id": "half",     "label": "Semi-Annually", "months": 6  },
    { "id": "annual",   "label": "Annually",      "months": 12 }
  ],
  "longStayDiscountPercent": 0,
  "rooms": [
    { "type": "ac",    "sharing": "Single", "monthly": 20000, "popular": false },
    { "type": "ac",    "sharing": "Double", "monthly": 12000, "popular": true  },
    { "type": "ac",    "sharing": "Triple", "monthly": 9000,  "popular": false },
    { "type": "nonac", "sharing": "Single", "monthly": 17000, "popular": false },
    { "type": "nonac", "sharing": "Double", "monthly": 9000,  "popular": true  },
    { "type": "nonac", "sharing": "Triple", "monthly": 7000,  "popular": false }
  ]
}
```

- `longStayDiscountPercent` is `0` until the client confirms a value (see README Section 2's open question). Build the calculation logic to support a discount now, even while the value is 0, so it's a one-line change later.
- Format all currency with `Intl.NumberFormat('en-IN')` so numbers group correctly (₹1,20,000, not ₹120,000).
- Render all four durations at build time and toggle visibility with a CSS class on the switcher — no client-side fetch, no flash of unstyled content.

WhatsApp links must be generated per room card with a pre-filled message, e.g.:

```
https://wa.me/916232880916?text=Hi%2C%20I%27m%20interested%20in%20Janki%20PG.%20Room%3A%20A%2FC%20Double%20Sharing
```

Build a small helper (`src/lib/whatsapp.ts` or similar) that takes a room label and returns this URL — don't hand-write the encoded string in every component.

---

## 6. Content and copy rules

- Placeholder content is fine early, but mark it clearly, e.g. `<!-- PLACEHOLDER: awaiting client address -->`, so nothing placeholder-ish accidentally ships.
- Do not invent specific facts not given (address, email, meal timings, visitor policy) — use clearly marked placeholders and flag them instead of guessing plausible-sounding details.
- Testimonials: 5–6 realistic sample entries are acceptable as placeholders, clearly marked as sample content to be replaced with real reviews before launch.
- Keep copy warm, plain, and specific. Avoid generic hostel-brochure language ("world-class amenities," "home away from home") in favor of concrete, checkable claims.

---

## 7. SEO requirements

- Use `LodgingBusiness` schema (not generic `LocalBusiness`) in `LodgingSchema.astro`, including `priceRange`, `amenityFeature`, and `checkinTime`/`checkoutTime` once known.
- Add `FAQPage` schema on the FAQ section.
- One clear primary keyword focus per page — do not stuff all target terms onto every page. Suggested assignment:
  - Home → "girls hostel", "girls PG"
  - Rooms & Pricing → "ladies PG price", "affordable girls PG"
  - About / House Rules → "safe girls accommodation"
- Title pattern: `Girls PG in [Area], Ahmedabad — A/C & Non-A/C Rooms | Janki PG`
- Every page needs a unique meta description, Open Graph tags, and a canonical URL via `BaseHead.astro`.
- Generate `sitemap.xml` via `@astrojs/sitemap` and a matching `robots.txt`.

---

## 8. Accessibility checklist (apply to every component)

- All interactive elements reachable and operable by keyboard
- Visible focus states — do not remove outline without replacing it
- Color contrast meets WCAG AA, especially on any glassmorphism panel
- All images have descriptive `alt` text (not filenames)
- Form fields have associated `<label>` elements, not just placeholder text
- Accordion and lightbox usable without JavaScript where feasible (native `<details>` for FAQ)

---

## 9. How to work

Build this site **one page or component group at a time**, not all at once. Suggested order:

1. Project scaffold — Astro + Tailwind config, `BaseLayout`, `Header`, `Footer`, design tokens in `tailwind.config.mjs`
2. `site.json`, `pricing.json` and the other data files, populated with the known information from README.md
3. Home page (`index.astro`) using placeholder sections first, then filled in
4. Rooms & Pricing page — build `PricingTable.astro` and its duration-switcher logic carefully; this is the most complex component in the project
5. Amenities, Gallery, FAQ
6. Enquiry form + Contact page
7. House Rules, Privacy Policy, Terms
8. SEO pass: schema, meta tags, sitemap, robots.txt
9. Accessibility and performance pass — target Lighthouse 95+ across the board

**After finishing each step, stop and show the result before moving to the next one.** Don't scaffold the entire site in one shot — this project is being reviewed incrementally, page by page, so each piece can be checked against the design direction before the next is built.

If a requirement in this file is ambiguous or missing information (address, exact colors, final copy), use a clearly marked placeholder and flag it rather than inventing a plausible-sounding answer.
