# Jordan Inspiration Tours

## Project Overview
- **Name**: Jordan Inspiration Tours
- **Goal**: A modern, fully responsive single-page marketing website for a Jordanian tourism company specializing in Petra trips, with complete Arabic/English bilingual support and dynamic RTL/LTR switching.
- **Features**:
  - Fully responsive (mobile-first) - flawless on phones, tablets, laptops and large desktops
  - Bilingual (English / العربية) with one-click language switcher
  - Automatic RTL/LTR direction switching
  - Hero section with Petra background + strong CTA
  - Tour Packages grid (Essential / Classic / Premium) with destinations, meals, hotels, transport & pricing
  - Tour Guide roster with live availability, star ratings, reviews and per-guide booking
  - Booking modal (date, time, guest count, notes) - opens from both packages and guides
  - Testimonials grid (international + local clients)
  - Footer with phone, email, social, address and working hours

## URLs
- **Local dev**: http://localhost:3000
- **Public sandbox**: (get via GetServiceUrl on port 3000)
- **Production**: (deploy to Cloudflare Pages via `npm run deploy`)

## Entry Points (routes)
| Path              | Method | Description                                              |
| ----------------- | ------ | -------------------------------------------------------- |
| `/`               | GET    | Full single-page website (all sections in one document)  |
| `/static/style.css` | GET  | Custom CSS (RTL rules, fonts, scrollbar, animations)     |
| `/static/app.js`  | GET    | Translations, language switcher, dynamic renderers, modal|
| `/favicon.svg`    | GET    | Branded SVG favicon                                      |

## Data Architecture
- **Data source**: Static, in-code JS data structures inside `/public/static/app.js`
  - `TRANSLATIONS` - EN/AR key-value dictionary (single source of truth for all UI copy)
  - `GUIDES` - array of guide objects with bilingual name / bio / review, photo, rating, availability
  - `TESTIMONIALS` - array of client testimonial objects with bilingual text
- **Storage services**: None (fully static site - no backend persistence yet)
- **Data flow**: Static data → JS renderer functions inject into DOM → language switcher re-renders

## User Guide
1. Open the site — English loads by default (or the last-used language from localStorage).
2. Click the **العربية / English** button (top-right of the navbar) to instantly translate the page and flip direction (RTL ⇄ LTR).
3. Scroll to **Packages** and click any **Book** button — a modal opens with the package name pre-filled.
4. Scroll to **Guides** — see each guide's live availability, star rating, spoken languages and a short review.
   - Available guides: click **Book this Guide** to open the modal with their name pre-filled.
   - Unavailable guides show a **Fully Booked** disabled state.
5. Fill in name, email, phone, date, time, number of guests and (optional) notes → submit → confirmation banner appears, modal auto-closes after 2.5s.

## How to Modify
- **Change / add translations**: edit `TRANSLATIONS` in `/public/static/app.js` (add a new key, then reference it via `data-i18n="your.key"` in `src/index.tsx`).
- **Add / edit / remove a guide**: edit the `GUIDES` array in `/public/static/app.js`.
- **Add / edit testimonials**: edit the `TESTIMONIALS` array in `/public/static/app.js`.
- **Update palette**: adjust the `petra` / `sand` colors in the `tailwind.config` block inside `src/index.tsx`.
- **Add your logo**: replace the `<!-- Logo Here -->` placeholder blocks in the navbar and footer (in `src/index.tsx`) with an `<img>` tag.

## Tech Stack
- **Runtime**: Cloudflare Pages / Workers
- **Framework**: Hono 4
- **Build**: Vite 6 (`@hono/vite-build/cloudflare-pages`)
- **Styling**: Tailwind CSS (CDN) with custom Petra + sand color palette
- **Icons**: FontAwesome 6
- **Fonts**: Playfair Display (EN headings) + Inter (EN body) + Cairo (Arabic)
- **JS**: Vanilla, no frameworks

## Deployment
- **Platform**: Cloudflare Pages
- **Status**: ✅ Running locally on port 3000 (via PM2)
- **Commands**:
  - Build: `npm run build`
  - Dev (PM2): `pm2 start ecosystem.config.cjs`
  - Deploy to CF Pages: `npm run deploy`
- **Last Updated**: 2026-07-06

## Currently Not Implemented (Recommended Next Steps)
- Backend `POST /api/bookings` endpoint to persist form submissions (D1 or third-party CRM)
- Email confirmation to the guest and internal notification (Resend / SendGrid)
- Real photo gallery / lightbox for each package
- Blog / travel guide articles
- Multi-currency price switcher (USD / EUR / JOD)
- Guide profile detail pages
- Reviews submission form for past customers
