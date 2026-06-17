# Uncle Inc. — Build Plan

## 1. PRODUCT

Uncle Inc. is an AI-assisted MVP platform that lets non-technical founders turn a written idea into a functional, testable prototype in hours, then validate it with real users and built-in analytics before writing a line of production code. The core value is collapsing the gap between "napkin sketch" and "evidence-backed go/no-go decision" — replacing gut-feel with real user signal in a 72-hour loop. The primary user is a solo or first-time technical co-founder-less founder who has an idea but no engineering bench, no design team, and no patience for a six-month build before knowing if anyone wants the thing. The pain it solves is the founder's classic trap: spending months (or money) building something nobody asked for, because the only way to test an idea today is to either code it yourself, hire a dev shop, or stare at a Figma file and hope.

## 2. WHO IT'S FOR

The ICP is a time-poor, non-technical first-time founder — typically a domain expert (consultant, operator, ex-corporate escapee) aged 28–45, working solo or with one non-technical co-founder, who has validated the problem anecdotally but has no engineering capacity. They are skeptical of "no-code" tools that produce toy apps, allergic to jargon, and want a single screen that tells them what to do next. This shapes the product: the landing page opens on a single, unambiguous value prop with one primary CTA ("Join the Waitlist"); the copy is plain-spoken and concrete (hours, not "10x faster"); pricing is three flat tiers with no "Contact Sales" gate; the FAQ answers the literal objections a non-technical founder types into Google ("Do I need coding skills?", "Can I export my code?"); and there are zero invented logos, testimonials, or user counts — because the ICP is exactly the kind of person who can smell fake social proof and bounces.

## 3. LOOK & FEEL

**Overall vibe / positioning:** Crisp Operator. Enterprise-clean, confident, slightly editorial. Reads like a serious tool for serious operators — not a hackathon project, not a consumer toy. Generous whitespace, precise 4px spacing grid, 1280px max container, 4px border-radius (sharp, not bubbly). The visual metaphor is a "switchboard" — clean panels, clear inputs/outputs, no decoration without function.

**Color palette (Tailwind tokens):**
- `navy` `#1A3A5C` — primary brand, headings, dark CTA section bg
- `cobalt` `#4A90D9` — secondary accent, links, focus rings, subtle highlights
- `slate` `#64748B` — secondary text, captions, muted labels
- `green` `#22C55E` — primary action, success, "Join Waitlist" buttons
- `surface` `#FFFFFF` — card backgrounds
- `bg` `#F8FAFC` — page background
- `dark` `#0F172A` — primary text
- `border` `#E2E8F0` — dividers, card borders, input borders

**Typography:**
- Headings: **Inter** (700/600), tight tracking, large scale (Hero h1 = `text-5xl md:text-6xl`)
- Body: **IBM Plex Sans** (400/500), comfortable line-height (`leading-relaxed`)
- Both loaded via `next/font/google` in `app/layout.tsx` with CSS variables `--font-inter` and `--font-plex`

**Spacing & layout:** 4px base unit. Sections separated by `py-20 md:py-28`. Container `max-w-7xl mx-auto px-6`. Cards use `border border-border bg-surface p-6` with `rounded` (4px). No drop shadows on cards — use a 1px border for the Crisp Operator feel; reserve shadow only for the sticky nav (`shadow-sm`).

**Iconography:** Inline SVG only, 1.5px stroke, `currentColor`, 24×24 viewBox. One icon per feature card, drawn in cobalt. No icon library dependency.

**Imagery:** None on the landing page. The product is the copy and the structure. No stock photos, no hero illustration, no fake dashboard screenshot — those would be invented specifics.

**Interaction & motion:** Minimal. FAQ items animate height with `transition-all duration-200`. Nav gets `shadow-sm` on scroll (optional, can be skipped for v1). Buttons have `transition-colors` only. No scroll-triggered animations, no parallax, no carousels.

---

### Screen-by-screen layout

**`Nav` (sticky, top of every page)**
- Sticky `top-0 z-50 bg-surface/90 backdrop-blur border-b border-border`
- Left: text wordmark "Uncle Inc." in `font-inter font-bold text-navy text-lg`
- Center (md+): three text links — Features, Pricing, FAQ — `text-sm text-slate hover:text-dark`
- Right: green button "Join Waitlist" `bg-green hover:bg-green/90 text-white text-sm font-medium px-4 py-2 rounded`
- Mobile: hamburger that toggles a stacked menu (state in `useState`)

**`Hero`**
- `pt-32 pb-24 md:pt-40 md:pb-32` on `bg-bg`
- Centered, max-w-3xl
- Eyebrow: `text-xs uppercase tracking-widest text-cobalt font-medium` — "AI-Assisted MVP Platform"
- H1: `font-inter font-bold text-4xl md:text-6xl text-dark leading-tight tracking-tight` — "Validate Your Startup Idea Before You Build It"
- Sub: `mt-6 text-lg md:text-xl text-slate leading-relaxed` — "AI-assisted MVP platform. Go from napkin sketch to tested prototype in 72 hours — no technical co-founder required."
- CTA row: `mt-10 flex flex-col sm:flex-row gap-3 justify-center`
  - Primary: `bg-green hover:bg-green/90 text-white font-medium px-6 py-3 rounded` — "Join the Waitlist"
  - Secondary: `border border-border bg-surface hover:bg-bg text-dark font-medium px-6 py-3 rounded` — "See How It Works" (anchor to `#features`)
- No metrics row. No logos. No "as seen in".

**`Features` (`#features`)**
- `py-20 md:py-28 bg-surface`
- Section header centered: eyebrow "Features", h2 `font-inter font-bold text-3xl md:text-4xl text-dark` — "Everything you need to validate and launch", sub `mt-4 text-slate max-w-2xl mx-auto`
- Grid: `mt-16 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6`
- 6 cards, each: `border border-border bg-surface p-6 rounded hover:border-cobalt transition-colors`
  - Top: 24×24 cobalt SVG icon
  - Title: `mt-4 font-inter font-semibold text-lg text-dark`
  - Body: `mt-2 text-sm text-slate leading-relaxed`
- Cards in order: AI Rapid Prototyping / Built-in User Testing / Launch Analytics / Guided Validation / No Code Required / Iterate with Data

**`Pricing` (`#pricing`)**
- `py-20 md:py-28 bg-bg`
- Same header pattern, h2 — "Simple, transparent pricing"
- Grid: `mt-16 grid grid-cols-1 md:grid-cols-3 gap-6 max-w-5xl mx-auto`
- 3 cards. Middle card (Builder) is visually emphasized: `border-cobalt` + small "Most popular" pill in cobalt
- Each card: `border border-border bg-surface p-8 rounded`
  - Plan name: `font-inter font-semibold text-lg text-dark`
  - Price: `mt-4 font-inter font-bold text-4xl text-dark` + `/mo` in `text-slate text-base font-normal`
  - Free plan shows `$0` with `/mo`
  - Feature list: `mt-6 space-y-3` with cobalt checkmark SVG + `text-sm text-slate`
  - CTA button full-width at bottom: `mt-8 w-full`
    - Explorer: outline `border border-border text-dark hover:bg-bg`
    - Builder: green `bg-green hover:bg-green/90 text-white`
    - Team: outline `border border-border text-dark hover:bg-bg`

**`FAQ` (`#faq`)**
- `py-20 md:py-28 bg-surface`
- Header centered, h2 — "Frequently asked questions"
- Container: `mt-12 max-w-3xl mx-auto divide-y divide-border border-y border-border`
- Each item: button (full width, `text-left py-5 flex justify-between items-center`) toggling a panel
  - Question: `font-medium text-dark`
  - Chevron SVG rotates 180° when open (`transition-transform`)
  - Answer panel: `pb-5 text-sm text-slate leading-relaxed` — conditionally rendered
- 6 items: What is Uncle Inc? / Do I need coding skills? / How does user testing work? / What happens after the free tier? / Can I export my code? / Is my data secure?

**`CTA` (dark band)**
- `py-20 md:py-28 bg-navy`
- Centered, max-w-2xl
- H2: `font-inter font-bold text-3xl md:text-4xl text-white` — "Stop Guessing. Start Validating."
- Sub: `mt-4 text-lg text-white/70` — "Join the waitlist and be first to validate your startup idea."
- Form row: `mt-8 flex flex-col sm:flex-row gap-3 max-w-md mx-auto`
  - Email input: `flex-1 px-4 py-3 rounded bg-white/10 border border-white/20 text-white placeholder:text-white/50 focus:outline-none focus:border-cobalt`
  - Submit: `bg-green hover:bg-green/90 text-white font-medium px-6 py-3 rounded`
- Form is a client component with `useState` for email + a `submitted` state that swaps the form for a "You're on the list — we'll be in touch." confirmation message. No backend wired in v1 (no fake API call promise); the submit handler just sets state and `console.log`s.

**`Footer`**
- `border-t border-border bg-surface`
- `py-8 max-w-7xl mx-auto px-6 flex flex-col sm:flex-row justify-between items-center gap-4`
- Left: `text-sm text-slate` — "© 2026 Uncle Inc."
- Right: three text links `text-sm text-slate hover:text-dark` — Privacy, Terms, Contact (anchor `#` for v1)

## 4. USER FLOWS

**Primary flow — Waitlist signup (the only conversion that matters on a pre-launch landing page):**
1. Land on `/` → Hero is above the fold, "Join the Waitlist" is the dominant green button.
2. Click "Join the Waitlist" in Nav or Hero → smooth-scrolls to the dark CTA section (`#cta`).
3. Enter email → click "Join Waitlist" → form swaps to confirmation message in place.
4. State: idle (empty input, button enabled) → submitting (button disabled, label "Joining…") → submitted (form replaced by "You're on the list — we'll be in touch." + "Add another email" link that resets state).

**Secondary flow — Self-serve information scan:**
1. Land on `/` → read Hero → click "See How It Works" → smooth-scrolls to `#features`.
2. Scan 6 feature cards → click "Pricing" in nav → smooth-scrolls to `#pricing`.
3. Compare three tiers → click "FAQ" in nav → smooth-scrolls to `#faq`.
4. Expand relevant questions (e.g., "Do I need coding skills?", "Can I export my code?") → click "Join Waitlist" in nav → smooth-scrolls to `#cta`.

**Mobile flow:**
1. Land on `/` → tap hamburger → menu slides down with Features / Pricing / FAQ / Join Waitlist.
2. Tap any link → menu closes, page scrolls to anchor.

All nav and CTA buttons are anchor links (`#features`, `#pricing`, `#faq`, `#cta`) — no routing, no auth, no broken promises.

## 5. PAGES / ROUTES

| Route | Purpose | Layout |
|---|---|---|
| `/` | Single-page marketing site | Nav → Hero → Features → Pricing → FAQ → CTA → Footer, stacked vertically, anchor-linked |

That's the entire site for v1. No `/blog`, no `/login`, no `/dashboard` — those are post-launch. The product goal is explicitly a marketing landing page.

## 6. CORE FEATURES

For this landing page, "features" are the marketing surface, not the product surface. Each is a real, concrete UI element:

1. **Sticky nav with anchor navigation** — `components/Nav.tsx`, client component, `useState` for mobile menu open/closed, `useEffect` to close menu on route hash change.
2. **Hero with dual CTA** — `components/Hero.tsx`, server component, two buttons: primary green "Join the Waitlist" (anchor `#cta`), secondary outline "See How It Works" (anchor `#features`).
3. **6-card feature grid** — `components/Features.tsx`, server component, renders a static array of 6 feature objects `{ icon, title, body }` mapped to cards. Icons are inline SVG components defined in the same file.
4. **3-tier pricing table** — `components/Pricing.tsx`, server component, renders a static array of 3 plan objects `{ name, price, features[], cta, highlighted }`. Middle plan gets a "Most popular" pill and a cobalt border.
5. **Expandable FAQ** — `components/FAQ.tsx`, client component, `useState<number | null>` tracking the open item index. Only one item open at a time (accordion behavior). Chevron rotates via `transform rotate-180` on the open item.
6. **Dark CTA band with email capture** — `components/CTA.tsx`, client component, `useState` for email value + submission state machine (`idle | submitting | submitted`). On submit: prevent default, simulate 400ms delay, set `submitted`, show confirmation. No network call in v1.
7. **Footer** — `components/Footer.tsx`, server component, static links.

## 7. DATA MODEL

No backend, no database, no API routes in v1. The only client-side state is:

- `Nav`: `mobileMenuOpen: boolean`
- `FAQ`: `openIndex: number | null` (0–5, or null)
- `CTA`: `email: string`, `status: 'idle' | 'submitting' | 'submitted'`

Static content lives as module-level constants in each component file (e.g., `const FEATURES = [...]` in `Features.tsx`, `const PLANS = [...]` in `Pricing.tsx`, `const FAQ_ITEMS = [...]` in `FAQ.tsx`).

## 8. AUTH

None. This is a pre-launch marketing landing page. There is no login, no signup, no dashboard, no protected route. The only "capture" is the waitlist email, which is client-side state only in v1 (no persistence, no Supabase, no NextAuth). When the product launches, auth will be added — but adding it now would be a dead button, which is worse than none.

## 9. FILES

```
package.json
next.config.js
tsconfig.json
tailwind.config.ts
postcss.config.js
app/layout.tsx
app/globals.css
app/page.tsx
components/Nav.tsx
components/Hero.tsx
components/Features.tsx
components/Pricing.tsx
components/FAQ.tsx
components/CTA.tsx
components/Footer.tsx
```

## 10. ACCEPTANCE

- [ ] `npm install` completes with no errors.
- [ ] `npm run dev` starts Next.js on `http://localhost:3000` with no console errors.
- [ ] `npm run build` completes successfully (TypeScript strict mode passes).
- [ ] Visiting `/` renders Nav, Hero, Features, Pricing, FAQ, CTA, Footer in that order, top to bottom.
- [ ] Nav is sticky and stays visible on scroll.
- [ ] Nav links (Features, Pricing, FAQ) smooth-scroll to the correct section anchors.
- [ ] "Join Waitlist" buttons (Nav + Hero) scroll to the CTA section.
- [ ] "See How It Works" button scrolls to the Features section.
- [ ] Features section shows exactly 6 cards in a 3-column grid on desktop, 2 on tablet, 1 on mobile.
- [ ] Pricing section shows exactly 3 cards; the Builder card has a cobalt border and "Most popular" pill.
- [ ] FAQ section shows exactly 6 items; clicking a question expands its answer and collapses any other open answer; chevron rotates.
- [ ] CTA section has a navy background, white headline, email input, and green submit button.
- [ ] Submitting the email form swaps the form for a confirmation message and does not reload the page.
- [ ] Footer shows "© 2026 Uncle Inc." on the left and Privacy / Terms / Contact links on the right.
- [ ] No fake testimonials, no invented user counts, no fake logos, no fake metrics anywhere on the page.
- [ ] Inter and IBM Plex Sans are loaded via `next/font/google` and applied via CSS variables.
- [ ] All Tailwind color tokens (`navy`, `cobalt`, `slate`, `green`, `surface`, `bg`, `dark`, `border`) are defined in `tailwind.config.ts` and used consistently.
- [ ] Mobile (≤640px): nav collapses to hamburger, all grids collapse to single column, no horizontal scroll.
- [ ] No external icon library; all icons are inline SVG.
- [ ] No dead links, no placeholder lorem ipsum, no "TODO" comments in shipped code.

FILES: ["package.json", "next.config.js", "tsconfig.json", "tailwind.config.ts", "postcss.config.js", "app/layout.tsx", "app/globals.css", "app/page.tsx", "components/Nav.tsx", "components/Hero.tsx", "components/Features.tsx", "components/Pricing.tsx", "components/FAQ.tsx", "components/CTA.tsx", "components/Footer.tsx"]