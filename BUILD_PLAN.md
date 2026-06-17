I'll build the Uncle Inc. landing page directly. Let me start by setting up the project structure and creating all the required files.

## 1. PRODUCT

Uncle Inc. is an AI-assisted MVP platform for startup founders. The landing page presents the product, communicates the value proposition, captures leads via a waitlist CTA, and surfaces pricing/feature details. It targets non-technical founders who need to move from idea to working MVP without hiring an agency or learning to code — the research notes emphasize a "crisp operator" archetype with switchboard motif, and the page must function as a marketing surface that converts visitors into signups.

## 2. WHO IT'S FOR

Solo founders and small founding teams (technical and non-technical) who have validated a problem and need a working MVP in days, not months. The design uses navy/cobalt/green for trust + energy, Inter for crisp UI text, IBM Plex Sans for editorial body copy, and a single primary CTA per scroll section — because the ICP is time-poor and will bounce if navigation is ambiguous.

## 3. LOOK & FEEL

**Vibe:** Crisp Operator — enterprise confidence, editorial whitespace, switchboard-inspired iconography (nodes, connections, signal motifs).

**Palette:** navy `#1A3A5C`, cobalt `#4A90D9`, green `#22C55E`, background `#F8FAFC`, surface white, text `#0F172A` / `#64748B`, border `#E2E8F0`.

**Type:** Inter (headings, UI, buttons) and IBM Plex Sans (body, long-form). Tight tracking on display sizes.

**Spacing/Layout:** 1280px container, 4px base unit, 80–96px section padding, 4px radius on cards/buttons, 1px borders.

**Components:** Buttons (primary cobalt, secondary outline, green CTA accent), feature cards with icon + heading + body, pricing tier cards, FAQ accordion, sticky nav.

**Motion:** Subtle fade-in-up on scroll, hover lift on cards, no heavy animation.

**Screens (all on single page):**
- **Nav:** Sticky white bar, Uncle Inc. wordmark left, anchor links (Features, Pricing, FAQ) right, green "Join Waitlist" button.
- **Hero:** Full-width navy gradient background, white headline "Ship your MVP in days, not months", IBM Plex subhead, two CTAs (primary green "Join the waitlist", secondary outline white "See how it works"), below a stylized switchboard graphic placeholder.
- **Features:** 6-card grid (AI scoping, auto-build, integrations, deploy, iterate, export), cobalt icon tiles, heading + 2-line description each.
- **Pricing:** 3 tiers (Solo free, Builder $49/mo, Studio $149/mo) — middle tier highlighted with cobalt border + "Most popular" badge.
- **FAQ:** 6 questions in accordion (What is Uncle Inc.? Do I need to code? …), IBM Plex body text.
- **CTA:** Full-width cobalt section, white headline, single green button → waitlist.
- **Footer:** Dark navy, two columns (Product, Company), copyright, social placeholders (no fake logos).

## 4. USER FLOWS

1. Land → read hero → click "Join the waitlist" → smooth-scroll to CTA section (anchor `#waitlist`).
2. Enter email in CTA form → submit → form replaces with "You're on the list. We'll be in touch." (client-side state, no backend wired).
3. Browse features → click nav "Pricing" → smooth-scroll.
4. Open FAQ item → toggle open/close.
5. Mobile: nav collapses to hamburger menu, single column layouts.

## 5. PAGES/ROUTES

- `/` — Single-page landing composing Nav, Hero, Features, Pricing, FAQ, CTA, Footer.

## 6. CORE FEATURES (on this page)

- Sticky nav with smooth-scroll anchor links and mobile hamburger toggle.
- Hero with gradient background, dual CTA, switchboard visual block.
- 6-feature card grid with icon + title + description.
- 3-tier pricing grid with highlighted middle tier.
- FAQ accordion with single-open behavior.
- Waitlist email form (client-side state: `idle | submitting | success | error`, no real backend call).
- Responsive layout (mobile single column, tablet 2-col, desktop 3-col grids).

## 7. DATA MODEL

Not applicable — static landing page. Form state is local React state only.

## 8. AUTH

None — landing page only, no auth surface.

## 9. FILES

See end.

## 10. ACCEPTANCE

- `npm install` succeeds, `npm run build` produces a clean Next.js production build with no errors.
- All 8 sections (Nav, Hero, Features, Pricing, FAQ, CTA, Footer, plus page entry) render at `/`.
- Navy/cobalt/green palette applied via Tailwind config; Inter + IBM Plex Sans loaded in `layout.tsx`.
- Mobile responsive (hamburger menu, stacked grids).
- No fake testimonials, no invented customer logos, no fabricated stats.
- Waitlist form shows success state on submit (no network call required).

Now writing the files.