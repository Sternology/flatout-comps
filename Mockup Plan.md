# Flat Out Competitions — Homepage Mockup Plan & Claude Code Build Brief

**Prepared by Chris, 13 May 2026**
**Target tool:** Claude Code
**Destination:** static Netlify deployment, single self-contained HTML file
**Status:** Stage 2 of 3. Stage 3 (final Claude Code prompt with image filenames + supplied logo) follows once ChatGPT image generation is complete.

---

## 1. Objective

Build a one-page, fully responsive, visually polished mockup homepage for a fictional UK competition / prize-draw site called **Flat Out Competitions**, the comps-site sister brand to **Flat-Out Media** (existing automotive media agency, flatoutmedia.org).

The mockup must **look** like a fully functioning competition site that has been live for some time. It must **not** actually take payment, run draws, or process accounts. Every interactive element is inert (hash anchors and disabled forms are fine).

The mockup is for two purposes:
1. To demonstrate to Adam what a "Polished Direct Response" comp site in his niche could look like, anchored to a brand he already understands.
2. To validate the design system before any real build is commissioned.

---

## 2. Skills Claude Code should invoke

Use the following skills in combination, in roughly this priority:

- **frontend-design** — production frontend quality, attention to spacing, typography, motion
- **impeccable** — taste-level polish, micro-details, no rough edges
- **taste** — composition, restraint, hierarchy
- **marketing-psychology** — apply the behavioural principles documented in §10 of this brief
- **page-cro** — CRO best practice for the buy flow and hero
- **copywriting** — for any unspecified microcopy, write in the brand voice (§5)

If Claude Code asks which skill to lead with, the answer is **frontend-design + impeccable** for build, **marketing-psychology + page-cro** for layout decisions.

---

## 3. The brand anchor

### Parent brand: Flat-Out Media (real)

- Automotive creative agency. Founded 2019. UK.
- Services: cinematic automotive video, automotive photography, photo retouching, graphic design, editorial / PR, social.
- Hero image on their site: vibrant orange Caterham-style race car on a wet UK race circuit, dramatic moody lighting.
- Tagline energy: "Stepping your automotive business up a gear".
- Logo: white wordmark "FLAT-OUT" with a circular dial / speedometer mark to the left. Logo file will be supplied at Stage 3.
- Tone: confident, insider, race-track-fluent, no-nonsense, "we live and breathe automotive".
- Co-collaborations include Ben Collins (ex-Stig) and Castle Combe Circuit, so the brand sits in the proper motorsport / specialist-car-media space, not the showroom space.

### New brand: Flat Out Competitions

- Positions as: the comp site built by people who actually understand cars, not another generic operator.
- Inherits the orange + black palette, the bold uppercase voice, and the speedometer / dial iconography from the parent.
- Uses the parent brand as its primary trust signal in lieu of decade-long track record.
- Mixes prize types: cars lead, but cash, watches, filmmaking gear, and tech are all in rotation. (See §8 for the actual lineup.)

---

## 4. Visual system

### Palette

| Token | Hex | Usage |
|---|---|---|
| `--ink` | `#0B0B0B` | Page background, primary surface |
| `--carbon` | `#161616` | Secondary surface, cards |
| `--steel` | `#222428` | Borders, dividers, raised surfaces |
| `--bone` | `#F5F2EC` | Primary body text on dark, headline white |
| `--mute` | `#9CA0A6` | Secondary text |
| `--flame` | `#F26A1F` | Primary brand colour, primary CTA |
| `--flame-2` | `#FF8A3C` | Hover / gradient stop |
| `--ember` | `#B83E0E` | Pressed state, danger |
| `--redline` | `#E33A28` | Urgency, "Closes Today" tags, countdown danger zone |
| `--check` | `#3FB964` | Verified, percentage-sold "safe zone" |

Pure black backgrounds (`#000`) should be avoided. Use `--ink` so subtle film-grain and gradients read correctly.

### Type

Use Google Fonts via `<link>`:

- **Display:** `Anton` (free, condensed, heavy) for hero headlines and section titles. Always SET IN UPPERCASE. Letter-spacing slightly tightened (`-0.005em`).
- **Body:** `Inter` 400 / 500 / 600 / 700.
- **Mono:** `JetBrains Mono` 500 / 700 — used for prices, countdown digits, ticket-remaining counts. Gives the digital-dashboard feel.

Type scale (rem, mobile-first):
- H1 display: 3.5rem → 6rem at desktop
- H2 section: 2rem → 3rem
- H3 card title: 1.125rem → 1.25rem
- Body: 1rem (16px)
- Small / meta: 0.825rem

Line-height: tight (1.05) on Anton displays; standard (1.55) on body.

### Iconography

- Use **Lucide icons** via CDN, never emojis.
- Custom flourishes: a tachometer / speedometer arc for the percentage-sold indicator (see §6 hero). This is the signature visual move that ties back to the Flat-Out dial logo.
- Chequered flag, stopwatch, ticket, flame, lightning-bolt icons used sparingly for category accents.

### Motion

- Subtle. No page-takeover animation. No 3D scroll effects.
- Cards: 200ms transform on hover, scale 1.02 + translate-y -2px + soft orange glow.
- CTAs: subtle 1.5s shimmer sweep on `:hover` and on continuous loop only for the hero CTA.
- Countdown digits: tick down every second, no animation other than the number change.
- Percentage-sold tachometer: animate from 0 to target value on viewport-enter, 1200ms `cubic-bezier(.2,.8,.2,1)`.
- Sticky top nav: appears with a 150ms fade after 80px scroll.

---

## 5. Voice & copy guidelines

Brand voice is **confident, race-fluent, dry-witted, no-fluff**. Sentences are short. No exclamation marks except in genuine urgency contexts (Closes Today, Final Hour). Uppercase used as a tool, not as decoration.

**Tagline:** `WIN LIKE YOU LIVE. FLAT OUT.`

**Sub-tagline:** Built by Flat-Out Media. Six years inside the UK car scene.

**Section heading samples (use these verbatim):**

- Hero kicker: `LIVE NOW · ENDS TUESDAY 21:00`
- Hero headline: `WIN THIS BAYSIDE BLUE R34 GT-R`
- Hero sub: `From £2.50 per ticket. Or enter free by post.`
- Hero CTA: `ENTER NOW`
- Stats strip headline: (no header; the stats themselves are the headline)
- Live competitions section: `CURRENTLY ON THE GRID`
- Closing-soon strip: `CLOSING TODAY`
- Instant wins: `INSTANT WINS`
- Winners: `WON · WITNESSED · DELIVERED`
- How it works: `HOW IT WORKS`
- Why-us block: `BUILT DIFFERENT`
- Parent-brand tie-in: `BACKED BY FLAT-OUT MEDIA`
- Footer brand line: `Flat Out Competitions Ltd · Co. [placeholder]`

**Copywriting rules:**
- Never use "amazing", "incredible", "unbelievable", "lucky winner".
- Do use specifics: car model, mileage, spec, registration year, condition.
- Show ticket price, percentage sold, and time-remaining on every card.
- Free postal entry must be visible from the homepage. Never bury it. (Section 339 compliance — see §11.)

---

## 6. Site structure — sections in order

Top to bottom, single page:

1. **Utility strip** (slim, above main nav)
2. **Main navigation**
3. **Hero** — headline competition (R34 GT-R)
4. **Trust strip** — "As featured in / Backed by" media row
5. **Stats panel** — numbers
6. **Currently On The Grid** — 6-card live competitions grid
7. **Closing Today** — horizontal-scroll urgency strip (re-uses 3-4 of the cards with countdown chips)
8. **Instant Wins** — teaser block, 3 mini cards
9. **Won · Witnessed · Delivered** — winners carousel
10. **How It Works** — 3-step explainer
11. **Built Different** — trust theatre block (4 reasons)
12. **Backed by Flat-Out Media** — parent brand tie-in block
13. **Footer** — big numbers, free entry, T&Cs, payments, social, company info, age-18 notice

---

## 7. Section-by-section specification

### 7.1 Utility strip
- Slim row, 32px tall on desktop. Background `--carbon`.
- Left: Trustpilot 5-star widget with "Excellent — 1,247 reviews" text (placeholder, looks real). Use the actual Trustpilot SVG logo with star group.
- Centre: rotating ticker (CSS marquee acceptable, slow): `🏁 Latest winner: James M, Manchester · won £5,000 cash · 11 May` / `🏁 Free postal entry available on every competition` / `🏁 Live draws every Friday 7pm on YouTube`.
- Right: `Account` and `Cart (0)` icon-text combos, inert links.

### 7.2 Main navigation
- 72px tall on desktop, 56px on mobile.
- Logo top-left (logo file supplied at Stage 3 — use a placeholder block sized 160 × 40 pixels reading "FLAT OUT COMPETITIONS" in Anton until then).
- Centre nav: `Competitions`, `Cars`, `Cash`, `Tech & Gear`, `Instant Wins`, `Winners`, `Live Draws`.
- Right: `Sign in` text link + `Join` orange button.
- Mobile: collapse to hamburger.
- Behaviour: sticky, with subtle 1px `--steel` bottom border that thickens to 2px after 80px scroll. Add slight background blur on scroll.

### 7.3 Hero
- Full-bleed background image: `hero-r34.jpg` (R34 GT-R in pit lane, see Image Prompts).
- Dark gradient overlay (left to right or top to bottom) bringing in `--ink` at 70% opacity on the text side so type stays legible.
- Hero is **80vh on desktop, 90vh on mobile**.
- Content stacks (mobile) or sits left-aligned in left third (desktop):
  - Kicker line: small orange uppercase `LIVE NOW · ENDS TUESDAY 21:00` (countdown live, real ticking clock — set end time to next Tuesday 21:00).
  - Headline: Anton 6rem `WIN THIS BAYSIDE BLUE R34 GT-R`.
  - Sub: 1.125rem `2002. 38,400 miles. NISMO-spec. Full UK registration. From £2.50 per ticket — or enter free by post.`
  - **Tachometer percentage-sold indicator** (the signature element):
    - Curved arc gauge, 220° sweep, 240px diameter on desktop.
    - Tick marks at 0, 25, 50, 75, 100. Numbers 0–100 around the outside in `JetBrains Mono`.
    - Needle made of two SVG paths (red base, orange tip).
    - Animates from 0% to target value (set to 73%) on viewport-enter.
    - Centre text: `73% SOLD` in Anton + `7,243 / 10,000 tickets` in mono below.
  - Primary CTA: `ENTER NOW` — `--flame` background, white text, Anton, 56px tall, slight 3D depth using inset highlight and external shadow.
  - Secondary text link directly below CTA: `Watch the prize walk-around (1:42)` — opens an inert YouTube-thumbnail-style modal placeholder.
  - Free entry line, very small, below: `No purchase necessary. Enter free by post — same odds.` linked to `#free-entry`.
- Bottom of hero: a thin row of "trust pellets" showing 4 icons + tiny labels: `LIVE DRAWS`, `CASHFLOWS SECURED`, `18+`, `FREE POSTAL ENTRY` — each 24px icon + 11px caption.

### 7.4 Trust strip
- Background `--ink`, 80px tall on desktop.
- Single row, 6 grayscale "as featured in" media logos: Top Gear, Performance Car, Goodwood, Castle Combe Circuit, Car Throttle, EVO. Use neutral placeholder boxes if Claude Code lacks SVGs — render as monospace text in mid-grey.
- Above the row, tiny eyebrow text centred: `AS COVERED BY`.

### 7.5 Stats panel
- Four columns on desktop, 2×2 on mobile. Background `--carbon`, 96px tall on desktop.
- Each cell: huge Anton number in `--flame`, label in mono below.
  - `£127,400+` / `GIVEN AWAY IN PRIZES`
  - `89` / `REAL WINNERS`
  - `4,200+` / `MEMBERS`
  - `4.9 / 5` / `1,247 REVIEWS`
- Numbers animate up from 0 on viewport-enter using a counter (300ms easing).
- These are intentionally believable launch-phase numbers, not BOTB-scale numbers. The credibility is borrowed from the parent brand, not faked.

### 7.6 Currently On The Grid (live competitions)
- Heading: Anton `CURRENTLY ON THE GRID` left-aligned, small orange eyebrow above reading `LIVE COMPETITIONS · 6 OPEN`.
- 6-card grid: 3 columns on desktop, 2 on tablet, 1 on mobile.
- Each card:
  - Top: prize image, 16:9 ratio.
  - Status chips overlaid on image top-left:
    - `CLOSING TODAY` red chip (for one or two cards)
    - `INSTANT WIN` blue chip (for one)
    - `JUST LAUNCHED` orange-outline chip (for one)
  - Body of card on `--carbon` surface:
    - Small mono price `£2.50 / TICKET` in `--flame`
    - Anton 1.25rem title (uppercase)
    - One-line spec or summary in body
    - Tachometer-mini (40px) showing % sold OR a horizontal "redline" progress bar styled as a rev-counter scale (segments going from white through orange to red as it approaches 100%)
    - `XX,XXX / YY,YYY tickets sold` in mono small below the bar
    - Countdown `2D 14H 22M` mono
    - CTA full-width button `ENTER` — secondary style (outline-orange-on-dark) for most, full orange for the urgent ones.
  - Card cards are below.

**The six competitions on the grid:**
| Slot | Prize | Price | Status chip | % sold | Closes |
|---|---|---|---|---|---|
| 1 | £10,000 TAX-FREE CASH | £1.00 / ticket | INSTANT WIN | 41% | 4D |
| 2 | SONY FX6 CINEMA CAMERA KIT (body + 3 primes + monitor + cage) | £4.99 / ticket | — | 28% | 9D |
| 3 | GOODWOOD TRACK DAY + CATERHAM 420R FOR 24 HRS | £3.50 / ticket | JUST LAUNCHED | 12% | 11D |
| 4 | LUXURY CHRONOGRAPH (panda-dial, steel) | £2.00 / ticket | CLOSING TODAY | 87% | 6H |
| 5 | HRE FORGED WHEELS — 4-WHEEL SET, CUSTOM SPEC | £1.50 / ticket | — | 64% | 3D |
| 6 | SNAP-ON LOADED ROLLER CABINET | £1.00 / ticket | — | 52% | 6D |

Image filenames listed in §8 should be inserted by Claude Code at Stage 3.

### 7.7 Closing Today strip
- Horizontal scroll, snap-points, 3 cards (using a subset of the six above plus duplicates if needed).
- Each card has a giant red countdown timer overlay in the bottom right.
- Background `--ink`. No grid heading needed; section title `CLOSING TODAY` in red Anton uppercase, with a stopwatch icon.

### 7.8 Instant Wins teaser
- 3 mini cards in a row on desktop, stack on mobile.
- Each card narrower than the main grid, e.g. 320px wide.
- Content: prize name, "INSTANT WIN" red-orange tag, price, "Win in seconds — no draw" line, CTA `PLAY`.
- Example prizes: `£500 IN YOUR ACCOUNT NOW`, `PS5 PRO BUNDLE`, `£250 CASH`.

### 7.9 Won · Witnessed · Delivered (winners)
- Heading Anton `WON · WITNESSED · DELIVERED`.
- Eyebrow: `RECENT WINNERS · DRAWS STREAMED LIVE`.
- 4-card carousel on desktop, 1-up on mobile with horizontal scroll.
- Each card: square photo placeholder (use generated portrait or a stylised initials avatar), name + town, prize won, comp name, date, small play-icon link "Watch the draw" (inert).
- Below the carousel: a thin row of 8 micro-avatars and the line `+ 89 more winners since launch · See them all →`.

### 7.10 How It Works
- 3 steps in a row on desktop, stack on mobile.
- Numbered `01 / 02 / 03` in Anton, large `--flame`.
- Step headings:
  1. `PICK YOUR PRIZE` — Browse open comps. Choose how many entries.
  2. `ANSWER THE SKILL QUESTION` — One simple question. Or enter free by post.
  3. `WATCH THE LIVE DRAW` — Every Friday 7pm on YouTube. Winners called immediately.
- Each step a 2-3 line description.
- Small footnote line beneath: `Section 339 compliant. Free postal entry on every competition.`

### 7.11 Built Different (trust theatre)
- 4 cards in a row on desktop, 2×2 on mobile.
- Each card has a lucide icon + heading + 2-line description:
  - `🎯 PROVABLY FAIR DRAWS` — Every draw is streamed live on YouTube. Random number generator output is published before and after.
  - `🚗 BACKED BY PETROLHEADS` — Run by the team behind Flat-Out Media — six years inside UK motorsport and tuner culture.
  - `📮 FREE TO ENTER` — Every competition has a no-purchase postal route with the same odds.
  - `🔒 CASHFLOWS SECURED` — FCA-regulated payment processing. Your money lands in protected accounts.

### 7.12 Backed by Flat-Out Media block
- Full-width band, 2-column layout on desktop. Left: text. Right: photo of the parent brand's race-team at work (Caterham at Castle Combe vibe).
- Eyebrow: `BACKED BY FLAT-OUT MEDIA`
- Headline: Anton — `THE COMP SITE WITH A PIT CREW`
- Body: 3 short sentences. "We are not a marketing agency that started doing comps. We are a creative team that has spent six years on track-day Tuesdays and pit-lane Fridays. The team behind our films, magazine features, and OEM work is the same team curating what we put up to win."
- CTA: `See Flat-Out Media's work →` linking to `https://flatoutmedia.org`.

### 7.13 Footer
- Background `--ink`. 5 columns on desktop, accordion-collapsed on mobile.
- Column 1: logo + tagline + the four big numbers from §7.5 restated as a stacked mini-block.
- Column 2: `COMPETITIONS` — Cars / Cash / Tech & Gear / Watches / Experiences / Instant Wins.
- Column 3: `INFO` — How It Works / Winners / Live Draws / Free Postal Entry (Section 339) / FAQs.
- Column 4: `LEGAL` — Terms & Conditions / Privacy / Cookies / Responsible Play / Complaints.
- Column 5: `CONTACT` — email, support hours, plus social row.
- Beneath all columns, a 1px `--steel` rule, then a 64px tall trust row: payment icons (Visa, Mastercard, Apple Pay, Google Pay, PayPal) + Cashflows logo + Age 18+ circle badge + Trustpilot 5-star widget.
- Bottom line: `© 2026 Flat Out Competitions Ltd · Company No. [placeholder] · Registered in England · Flat Out Competitions is part of the Flat-Out Media group. 18+ only. Please play responsibly. BeGambleAware.`

---

## 8. Image inventory

All images sit in `/img/` relative to `index.html`. ChatGPT-generated, JPG, sRGB, quality 80. The image prompts file in this folder gives the prompts.

| Filename | Subject | Aspect | Where used |
|---|---|---|---|
| `hero-r34.jpg` | Modified Bayside Blue R34 GT-R, pit lane at twilight | 21:9 cinematic | §7.3 hero |
| `card-cash.jpg` | Stacked £50 notes with watch box + key fob | 4:3 | §7.6 card 1, §7.7 |
| `card-camera.jpg` | Cinema camera + lens kit flat-lay | 4:3 | §7.6 card 2 |
| `card-trackday.jpg` | Lightweight orange roadster mid-corner on a circuit | 4:3 | §7.6 card 3 |
| `card-watch.jpg` | Panda-dial chronograph macro on slate | 1:1 | §7.6 card 4 |
| `card-wheels.jpg` | Set of four forged bronze wheels in studio | 4:3 | §7.6 card 5 |
| `card-tools.jpg` | Glossy red tool chest in workshop | 4:3 | §7.6 card 6 |
| `logo-foc-white.svg` | Flat Out Competitions logo (supplied at Stage 3) | — | §7.2 nav |
| `parent-team.jpg` *(optional)* | Behind-the-scenes shot of car-shoot or pit-lane | 16:9 | §7.12 |

Winner portrait placeholders can be generated styled initials in coloured circles via CSS — no images required.

---

## 9. Interaction & motion specification

- All countdowns are real: pick three different end-times in JS (next Tuesday 21:00 UK for hero; varied days/hours for cards) and tick the digits in real time.
- All percentage-sold gauges animate on viewport-enter using IntersectionObserver, single-shot.
- Hero CTA shimmers continuously, 1.5s diagonal sweep, low opacity (10%).
- Cards: 200ms `transform: translateY(-2px) scale(1.02);` + 0–8px orange glow on `:hover`, with a 240ms reverse easing on `:not(:hover)`.
- Sticky nav: subtle backdrop-filter blur(10px) after 80px scroll; border-bottom transitions from 1px to 2px.
- Mobile menu: slide-in from right, full-height drawer, with a chequered-flag motif as a 6px tall top border.
- "Live now" pulsing dot next to the hero kicker: 1.5s pulse animation, infinite.
- Marquee in utility strip: pure CSS keyframe animation, paused on hover.
- All hover and focus states must be keyboard-navigable.

---

## 10. Marketing psychology & CRO principles to bake in

Embed these without explicit reference in copy — they are structural:

- **Scarcity:** Percentage-sold gauges and ticket-remaining counters surfaced on every card, not buried.
- **Time pressure:** Live ticking countdowns, "CLOSING TODAY" red chips, urgency strip.
- **Social proof:** Trustpilot widget in three places (utility strip, why-us, footer), winners section with photos and named places, "+89 more winners" pellet.
- **Authority transfer:** "Backed by Flat-Out Media", "as featured in" media logos, Ben Collins / Goodwood / Castle Combe associations.
- **Loss aversion:** "Tickets sold" presented as `X / Y` with the remaining gap visible (not just %).
- **Anchoring:** Ticket prices from £1, but the prize values implied are five-figure-plus.
- **Reciprocity / fairness signal:** Free postal entry surfaced in the hero, in step 2, in the trust block, in the footer.
- **Transparency:** "Provably fair draws" with the RNG-published-before-and-after promise.
- **Risk reversal:** "Cashflows secured" badge implying regulated payments.
- **Identity priming:** "Built by petrolheads, for petrolheads" + automotive media tie-in. The target buyer should feel they have found *their* comp site, not a generic one.

---

## 11. Compliance elements (Section 339, Gambling Act 2005)

- **Free postal entry route** must be linked from the hero, from step 2 of "How it works", from the "Built different" block, and from the footer. Anchor `#free-entry` is acceptable for the mockup; in production this would be a full page.
- **Age 18+** badge in the footer trust row and in the utility strip on mobile.
- **Skill question** mentioned in How It Works step 2.
- **BeGambleAware** link in the footer base line.
- **Responsible Play** link in the footer Legal column.
- No mockup copy should make claims a real comp site could not back up ("guaranteed to win", etc.).

---

## 12. Accessibility & performance baseline

- Lighthouse mobile target: **Performance 90+, Accessibility 95+, Best Practices 95+, SEO 90+.**
- All interactive elements keyboard-focusable with visible focus rings (`--flame` 2px outline + 2px offset).
- Colour contrast ≥ 4.5:1 for body, ≥ 3:1 for large text.
- All images need real `alt` attributes describing the prize.
- Semantic HTML: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>` (per competition card), `<footer>`.
- `<meta name="viewport" content="width=device-width, initial-scale=1">` and proper `lang="en-GB"`.
- Inline critical CSS, defer everything else.
- Preload hero image.
- Images use modern `<img>` with `loading="lazy"` (except hero, which should be eager + fetchpriority="high").
- Use `srcset` for the hero if you generate multiple sizes.

---

## 13. Technical constraints for Claude Code

- **Single self-contained `index.html` file** in the project root, plus an `/img/` folder for the photographs. CSS and JS inline within the HTML. No build step. No package.json. Anyone can clone the folder and double-click `index.html`.
- **Tailwind CSS via CDN** (Play CDN is acceptable for mockup purposes — note this in a comment as not production-ready).
- **Google Fonts** loaded via single `<link>` for Anton, Inter, JetBrains Mono.
- **Lucide icons** loaded via CDN (`https://unpkg.com/lucide@latest`).
- **No build tools.** No npm, no Vite, no Next.js.
- **No analytics, no tracking pixels.**
- **All forms inert** — `preventDefault` on submit and show a small "Mockup only — form disabled" inline toast.
- All competition CTAs go to `href="#"` with an `onclick` that shows the same inline toast.
- Target browsers: latest Chrome, Safari, Firefox, Edge. No IE.
- Mobile breakpoints: `sm:` 640px, `md:` 768px (this is the primary tablet/desktop split), `lg:` 1024px, `xl:` 1280px.
- File size budget: HTML+CSS+JS combined ≤ 80KB minified (images excluded).

---

## 14. Research embedded — what makes this design language right

This brief assumes the recommendations in the companion documents `Competition Site Research - for Adam.pdf` and `Design Psychology Brief - for Adam.pdf`. The short version:

- **"Polished Direct Response" wins this category.** Not Apple-style minimalism. Not under-designed amateur. A polished casino-floor energy: warm urgent colours, percentage-sold bars, countdown timers, dense social proof, trust badges visible immediately.
- **The market leaders (BOTB, Dream Car Giveaways) are polished but loud.** £29m revenue and £193m given away respectively. Neither is minimalist.
- **Niche operators (LLF Games, Camera Competitions) turn the volume up further, not down**, because they have less trust capital than the household-name mainstream players. Flat Out Competitions is in that niche tier and should behave accordingly.
- **The audience-first pattern.** Every successful niche operator has an audience-first asset (LLF Games = automotive YouTube; Camera Competitions = a 50-year-old camera retailer). Flat Out Competitions has Flat-Out Media. The site is the conversion engine; the audience comes from the parent brand.
- **Trust theatre is the conversion mechanism, not decoration.** Live winner feeds, big numbers, Trustpilot, transparency about the RNG, live Facebook / YouTube draws, free entry route, real address — these are not optional.
- **Spiky traffic is the failure mode.** The mockup does not need to handle it, but the design must surface the urgency cues (countdowns, % sold) that drive that traffic shape in the first place.

---

## 15. Acceptance criteria

The mockup is finished when:

- [ ] A first-time viewer landing on the page believes within 5 seconds that this is a real live comp site.
- [ ] The brand sits cleanly with Flat-Out Media's existing identity — palette, type, voice, energy.
- [ ] Every section described in §6 / §7 is present, in order.
- [ ] The seven listed prizes are all on the page with the spec from §7.6.
- [ ] Tachometer percentage-sold indicator animates on viewport-enter and is visually anchored to the dial motif of the parent brand.
- [ ] All countdowns tick down in real time.
- [ ] Lighthouse mobile scores hit the §12 targets.
- [ ] Mobile view (375 wide) is fully usable and visually coherent.
- [ ] No console errors, no broken links beyond the inert `#` anchors.
- [ ] Free postal entry route is visible from the hero and footer.
- [ ] 18+ notice and BeGambleAware link are in the footer.

---

## 16. What I still need from Adam / Chris (Stage 3 inputs)

To turn this plan into a final Claude Code build prompt, I still need:

1. The **logo file** (PNG or ideally SVG) for Flat Out Competitions (or the parent FOM logo recoloured / relabelled).
2. The **seven generated images** from the Image Prompts document, saved into `/img/` with the filenames listed in §8.
3. *(Optional)* a preferred company-number placeholder for the footer.

Once those land, the final Claude Code prompt is essentially this document + image references + the logo, with a wrapper instructing Claude Code to invoke the skills listed in §2.

---

## 17. Companion documents

- `Image Prompts.md` — same folder. Seven ChatGPT image generation prompts, ready to paste.
- `../Competition Site Research - for Adam.pdf` — full platform research.
- `../Design Psychology Brief - for Adam.pdf` — full design psychology brief, including niche-vs-mainstream commentary.
