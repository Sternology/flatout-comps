# Claude Code Build Prompt — Flat Out Competitions Homepage Mockup

> Paste everything from "START OF PROMPT" below into Claude Code, running in this folder (`Mockup/`). Claude Code should also be told to read `Mockup Plan.md` (in the same folder) for the full structural spec — this prompt is the wrapper that authorises the build and supplies the asset filenames.

---

## START OF PROMPT

You are building a single-file, self-contained, fully responsive HTML homepage mockup for a fictional UK competition / prize-draw site called **Flat Out Competitions**. The deliverable is one `index.html` file plus the existing `img/` folder of assets, ready to be uploaded to Netlify as a static site.

Before writing any code, read **`Mockup Plan.md`** in this folder end-to-end. That document is the complete structural and visual specification. Treat it as canonical. Everything below is the wrapping context.

### Skills to invoke

Use the following skills in combination, applied in roughly this order:

1. **frontend-design** — overall build, structure, spacing, type, responsiveness
2. **impeccable** — taste-level polish, micro-details, no rough edges
3. **taste** — composition, restraint, hierarchy decisions
4. **marketing-psychology** — apply persuasion principles (scarcity, urgency, social proof, authority transfer, loss aversion) as structural choices, not just copy
5. **page-cro** — hero, CTAs, trust theatre placement, friction reduction
6. **copywriting** — for any microcopy not explicitly given in the Plan, write in the brand voice defined in §5 of the Plan

If forced to pick a lead skill: **frontend-design + impeccable** for build, **marketing-psychology + page-cro** for layout decisions.

### What this site is

Flat Out Competitions is the comp-site sister brand to **Flat-Out Media** (real automotive media agency, flatoutmedia.org), founded 2019, based in the UK, doing cinematic automotive content for OEMs, magazines, Castle Combe Circuit, and Ben Collins (ex-Stig). The comp site inherits the parent brand's vibrant orange + matte black palette, bold uppercase typography, and dial / speedometer iconography. It positions as the comp site built by petrolheads, for petrolheads, in contrast to the dated WordPress comp sites and the generic mainstream players.

The buyer is a UK car enthusiast in their 20s-40s, sitting on the sofa watching TikTok, spending £1-5 a ticket. They are buying a fantasy with pocket change. The site must feel polished but loud, with the energy of a casino floor: warm urgent colours, prize photography, percentage-sold gauges, countdown timers, dense social proof, trust badges visible immediately. **Not Apple-style minimalism. Not under-designed.** Read §10 of the Plan for the full psychological rationale.

### The signature design move

The percentage-sold indicator throughout the site is rendered as a **curved tachometer / speedometer arc gauge**. This is the most-used UI element on a comp site, and turning it into a branded dial directly references the parent brand logo (see `img/logo-foc.png` — the dial is part of the wordmark). The hero gauge is large (220px+ diameter, 220° sweep, tick marks, animated needle). Card gauges are mini versions (40-60px). Read §7.3 of the Plan for the full hero spec, and §4 for typography and colour tokens.

### Asset inventory (all already in `img/`)

| Filename | What it is | Used in |
|---|---|---|
| `img/logo-foc.png` | Flat Out Competitions logo: white "FLAT-OUT" wordmark with a circular speedometer dial mark, red "COMPETITIONS" subtitle, on a black backdrop | Nav (top-left), footer |
| `img/hero-r34.png` | Bayside-blue Nissan Skyline R34 GT-R in a darkened pit lane at night, dramatic lighting, wet reflections | Hero |
| `img/card-cash.png` | Stacked British £50 notes with watch box and key fob, moody product shot | Live-comp card 1 (£10,000 CASH) |
| `img/card-camera.png` | Cinema camera flat-lay with three lenses, monitor, cage, battery on charcoal concrete | Live-comp card 2 (CINEMA CAMERA KIT) |
| `img/card-trackday.png` | Orange Caterham-style roadster in mid-corner at golden hour, motion-blurred background | Live-comp card 3 (GOODWOOD TRACK DAY) |
| `img/card-watch.png` | Panda-dial steel chronograph on dark slate, macro shot | Live-comp card 4 (LUXURY CHRONOGRAPH) |
| `img/card-wheels.png` | Four bronze forged multi-spoke wheels with yellow brake calipers visible | Live-comp card 5 (HRE FORGED WHEELS) |
| `img/card-tools.png` | Glossy red roller tool chest with chrome top, drawer open showing sockets, workshop background | Live-comp card 6 (SNAP-ON ROLLER CABINET) |
| `img/parent-team.png` | Behind-the-scenes shot: small film crew shooting an orange Caterham in a UK pit-lane garage | "Backed by Flat-Out Media" parent-brand tie-in block (§7.12) |

**Important:** assets are PNG, not JPG (the Plan mentions JPG in places — that's outdated; use the actual `.png` filenames above).

### Logo handling

The supplied logo (`img/logo-foc.png`) has a pure black background baked in. Two acceptable ways to handle this:

1. **Preferred:** apply CSS `mix-blend-mode: lighten` to the `<img>` tag. Against the matte-black nav (`#0B0B0B`) this will make the black backdrop invisible while preserving the white wordmark, red sub-wordmark, and the dial mark.
2. **Fallback:** set the nav background to pure `#000` in the area immediately surrounding the logo so the black backdrop blends seamlessly. Less elegant but reliable.

The logo should display at approximately 160px wide × 40px tall in the desktop nav, scaling to 130 × 32px on mobile. In the footer, slightly larger (180-200px wide).

### Build constraints

- **One file:** `index.html` in the Mockup folder root. All CSS and JS inline. No build step, no `package.json`, no bundler.
- **Tailwind via Play CDN** is acceptable for this mockup. Comment in the HTML that this is not production-ready.
- **Google Fonts** in a single `<link>` for Anton, Inter, JetBrains Mono.
- **Lucide icons** via CDN (`https://unpkg.com/lucide@latest`). No emoji icons.
- **No real backend, no analytics, no tracking pixels, no third-party scripts beyond the above.**
- **All forms inert.** `preventDefault` on submit and show a small inline toast that says "Mockup only — form disabled".
- **All CTAs** are `href="#"` with an `onclick` that triggers the same toast.
- **Mobile responsive.** Breakpoints `sm:640`, `md:768` (primary split), `lg:1024`, `xl:1280`. Test mentally at 375 (iPhone), 768 (tablet), 1440 (desktop).
- **Lighthouse mobile targets:** Performance 90+, Accessibility 95+, Best Practices 95+, SEO 90+.
- **File size budget:** HTML+CSS+JS combined ≤ 80KB minified, images excluded.
- **Semantic HTML:** `<header>`, `<nav>`, `<main>`, `<section>`, `<article>` (per competition card), `<footer>`.
- **`lang="en-GB"`** on `<html>`.
- **Hero image** preloaded with `fetchpriority="high"`. All other images `loading="lazy"`.
- **Keyboard navigation** must work end-to-end. Visible focus rings on every interactive element (2px `--flame` outline with 2px offset).

### The hero gauge specifically (because it is the signature element)

- Pure SVG, no external graphic.
- 240px diameter on desktop, 180px on mobile.
- 220° arc sweep (from -200° to +20° in standard math orientation, or whichever maths gets you a wide-bottom dial like a real tachometer).
- Tick marks every 10%, labelled 0 / 25 / 50 / 75 / 100 in JetBrains Mono.
- The arc itself transitions colour from `--bone` at the start, through `--flame` mid-way, to `--redline` at the top end.
- Needle: thick red base, orange tip, with a small white centre cap.
- Centre text: huge Anton number ("73%") with "SOLD" in mono below, plus "7,243 / 10,000 tickets" small mono below that.
- Animates from 0 to 73% on viewport-enter using IntersectionObserver, 1200ms cubic-bezier(.2,.8,.2,1).
- Mini-card gauges follow the same logic but at 48-60px diameter and without the centre text — just the needle and arc.

### Section ordering (recap — full detail in Plan §6–§7)

1. Utility strip (Trustpilot, marquee ticker, account/cart) — §7.1
2. Sticky main nav with logo, centre links, Sign in + Join — §7.2
3. Hero: R34 GT-R with kicker, headline, sub, tachometer gauge, primary CTA, free-entry line, trust pellets — §7.3
4. "As covered by" trust strip — §7.4
5. Stats panel: £127,400+ / 89 / 4,200+ / 4.9 — §7.5
6. CURRENTLY ON THE GRID — 6-card live competitions grid with the specific prizes in §7.6 — §7.6
7. CLOSING TODAY — horizontal-scroll urgency strip — §7.7
8. INSTANT WINS teaser (3 mini cards) — §7.8
9. WON · WITNESSED · DELIVERED — winners carousel with initials-avatar placeholders — §7.9
10. HOW IT WORKS — 3 numbered steps — §7.10
11. BUILT DIFFERENT — 4 trust-theatre cards — §7.11
12. BACKED BY FLAT-OUT MEDIA — parent brand tie-in block using `img/parent-team.png` — §7.12
13. Footer with 5 columns, payment row, age 18+, BeGambleAware — §7.13

The exact copy for each section is in the Plan. Use it verbatim. For any microcopy not specified, write in the voice defined in §5: confident, race-fluent, dry-witted, short sentences, uppercase used as a tool not a decoration.

### Acceptance criteria (the Plan's §15 restated for emphasis)

- A first-time viewer believes within 5 seconds that this is a real live comp site.
- The brand sits cleanly with Flat-Out Media's existing identity.
- Every section described in §6 / §7 of the Plan is present, in order.
- All seven prizes (hero R34 + six grid cards) are visible with the specs in §7.6 of the Plan.
- The tachometer percentage-sold gauge animates on viewport-enter and is visually anchored to the parent brand dial motif.
- All countdowns tick down in real time (set end times across the next 1–11 days for variety).
- Lighthouse mobile scores hit the §12 targets.
- Mobile view at 375px wide is fully usable and visually coherent.
- No console errors. No broken links beyond the inert `#` anchors.
- Free postal entry route is visible from the hero AND the footer.
- 18+ notice and BeGambleAware link present in the footer.
- The page should be self-contained — open `index.html` directly in a browser (file://) and everything works, including animations and countdowns.

### Working approach

1. Read `Mockup Plan.md` end-to-end. Do not skim. The Plan has the actual copy, the actual prizes, the actual section ordering, the actual psychology, and the actual compliance placements.
2. Sketch the page mentally before writing. Lock the section order and the rough vertical rhythm first.
3. Build the tachometer SVG component first as a standalone element — get the arc, ticks, needle, animation working before integrating into the hero.
4. Build the hero next, including the inline countdown JS.
5. Build the live-comp card component as a reusable HTML pattern — same markup six times with different content.
6. Build the remaining sections in order.
7. Add the footer.
8. Mobile pass: walk through at 375 / 768 / 1440 and fix any issues.
9. Accessibility pass: keyboard nav, focus rings, alt text on every image, colour contrast check.
10. Output `index.html` and confirm the file is self-contained.

### One last thing

This mockup will be sent to Adam (the prospect) to demonstrate what a properly-designed comp site in his niche could look like. The visual quality bar is "good enough that Adam looks at this and thinks 'this is what I want to build'." Do not phone in any section. Do not use lorem ipsum. Every prize, every winner name, every stat must look real. If a placeholder is unavoidable (winner avatars, for example), make the placeholder visibly intentional and considered, not a stock-grey square.

If anything in the Plan conflicts with your design judgement, follow the Plan. If anything in the Plan is genuinely ambiguous, make a confident decision and note it in a comment at the top of `index.html`.

Ship `index.html`. That is the deliverable.

## END OF PROMPT

---

## Quick reference for Chris before pasting

- **Open Claude Code in:** `C:\Users\chris\Phase 2\Prospects\Adam - Competition Site Research\Mockup\`
- **Plugins/skills expected:** frontend-design, impeccable, taste, marketing-psychology, page-cro, copywriting
- **Assets are already in place:** `img/` folder has all 9 images (1 logo + 1 hero + 6 cards + 1 parent-team)
- **Expected output:** a single `index.html` in the Mockup folder root
- **To preview:** double-click `index.html` and it should run without any local server, but Netlify deploy is the intended final step
- **If Claude Code asks anything load-bearing:** the answer is in `Mockup Plan.md` — point it back there.
- **If you want to iterate:** after the first build, the natural next prompts are "tighten the hero gauge", "make the stats counter animation snappier", "add a subtle film grain to the hero background", "rework the parent-brand block to be more cinematic".
