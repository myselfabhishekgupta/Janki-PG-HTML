# Plan: Update Janki PG Address

Update the address of "Janki PG" from "Mayur Vihar Phase 3, Delhi" to "Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi" across the website.

## Analysis of Occurrences

The string "Mayur Vihar Phase 3, Delhi" appears in:
1.  **Footer/Address sections**: All 7 pages.
2.  **Page Titles (`<title>`)**: `index.html`, `about.html`, `amenities.html`, `contact.html`, `gallery.html`.
3.  **Meta Titles (`og:title`)**: `index.html`, `about.html`, `amenities.html`, `contact.html`, `gallery.html`.
4.  **Meta Descriptions**: `index.html`, `rooms-and-pricing.html` (as placeholders).
5.  **Body Text**: `index.html` (line 155).

## Implementation Strategy

### 1. Full Address Updates (High Priority)
Replace "Mayur Vihar Phase 3, Delhi" with "**Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi**" in the following locations:

- **Footer/Address (`<p>` tags)**:
    - `index.html` (Line 720)
    - `about.html` (Line 352)
    - `amenities.html` (Line 449)
    - `contact.html` (Line 242)
    - `gallery.html` (Line 235)
    - `house-rules.html` (Line 305)
    - `rooms-and-pricing.html` (Line 509)
- **Body Text**:
    - `index.html` (Line 155): `Girls PG · Mayur Vihar Phase 3, Delhi` -> `Girls PG · Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi`

### 2. SEO-Sensitive Updates (Recommendation)
For the following, I recommend **keeping the area name** ("Mayur Vihar Phase 3, Delhi") to maintain SEO visibility for broader local searches:
- `<title>` tags
- `<meta property="og:title">` tags

**Reasoning**: Users searching for "Girls PG in Mayur Vihar Phase 3" are more likely to find the site if the title remains concise and targets the area name rather than a specific plot/flat number.

### 3. Placeholder Updates
Update the placeholder meta descriptions to reflect the updated address:
- `index.html` (Lines 20, 25)
- `rooms-and-pricing.html` (Lines 20, 25)

## Detailed File Changes

| File | Line(s) | Original String | Replacement String |
| :--- | :--- | :--- | :--- |
| `index.html` | 155 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `index.html` | 720 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `about.html` | 352 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `amenities.html` | 449 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `contact.html` | 242 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `gallery.html` | 235 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `house-rules.html` | 305 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `rooms-and-pricing.html` | 509 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `index.html` | 20, 25 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |
| `rooms-and-pricing.html` | 20, 25 | `Mayur Vihar Phase 3, Delhi` | `Pocket D, SFS Flats, Mayur Vihar Phase 3, Delhi` |

