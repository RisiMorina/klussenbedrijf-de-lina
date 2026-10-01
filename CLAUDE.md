# Klussenbedrijf De-Lina — website

One-page site for Edward, a one-man painter/handyman (schilderwerk, sauzen, stucwerk, tapijt, laminaat).
The site exists to make visitors **call Edward**. Nothing else.

## Source of truth

`de-lina-design.md` is the design document. It wins over any skill or default. Read it before changing anything.

## Files

```
index.html         the whole site — HTML, CSS and JS inline, no build step
de-lina-design.md  design doc: copy, sections, tokens, motion, never-do list, open questions
CLAUDE.md          this file
```

Open `index.html` directly in a browser. No dependencies except Google Fonts (Archivo wdth 85 / 800, Public Sans 400/600).

## Page structure (in order)

1. `header.nav`: "De-Lina" + "Bel Edward". Hides on scroll down, returns on scroll up or after 700ms idle.
0. `div.intro` (first in `<body>`): SVG brush-stroke intro overlay + its inline script. Shown only when the head script adds `html.has-intro` (first visit per session, no reduced motion). Removed from the DOM when done or skipped.
2. `section.hero`: h1 (6 words), sub line, `.actions`. No animation in the hero.
3. `section.services`: "Wat ik doe", `.lead`, plain `ul.list` (not cards), `.cta` with Bel Edward.
4. (Work section deliberately absent until real photos exist; see HTML comment TODO.)
5. `section.price`: "Eerlijke prijs".
6. `section.contact` (`--wall` band): lead, large `.phone` number (must stay visible as text for desktop users), Bel Edward + e-mail row, Werkgebied TODO.
7. `footer`: name, Edward, KvK TODO.
8. `.callbar`: mobile only (≤640px), fixed bottom Bel Edward + WhatsApp, appears once the hero is scrolled past.

## Conventions

- **All copy is Dutch**, written as Edward ("ik", "u"). Max 2 short sentences per section, no paragraph over 3 lines on desktop.
- **"Bel Edward"** appears in nav, hero, after services, contact (+ mobile call bar). Always `tel:+31642920203`.
- E-mail `mailto:hayk23@hotmail.nl`; WhatsApp `https://wa.me/31642920203`.
- **Tokens only** (in `:root`): `--plaster --wall --ink --muted --tape --tape-dark --line --line-soft`,
  `--text-lead`, `--btn-h`, `--measure` (60ch), `--gutter`, `--section`, `--nav-h`, `--torn` (tape clip-path).
  Do not add colours. No gradients, shadows, rounded cards.
- Text links use `--tape-dark` (not `--tape`) for AA contrast on plaster.
- Headings: `.taped` span inside each h2 draws the painter's-tape strip (`::before`). It's the one bold element; keep everything else quiet.
- Buttons: `.btn` (solid tape, 3px radius, `--btn-h`); `.nav .btn` is the only slimmer variant. No arrows in labels.
- Motion only runs under `html.motion` (set in the head script when JS runs and reduced motion is off). Without it everything is static and visible.
  - `.reveal`: fade + drift up, staggered via one running queue (`--d`, 110ms steps, capped at 550ms).
  - `h2[data-split]`: JS splits the heading into `.line` masks after the web font loads (re-split on width change); `.taped::before` draws in after (`--tape-delay`).
  - Hero `.wrap` parallax (translate 0.22× scroll) + `h1`/`.sub` fade to 0.45. `[data-parallax]` images drift inside `.work-photo` frames.
  - Lenis 1.3.26 (jsDelivr, SRI hash) is injected only on `(hover: hover) and (pointer: fine)`; it's available as `window.lenis`.
  - Never put `.reveal` on anything containing a `tel:` link or "Bel Edward": those must never be hidden or delayed.
  - Only animate `transform` and `opacity`.
- Intro: paint stroke 0–820ms, page opening behind it 150–950ms, opening grows to full screen 950–1250ms. Keep total under 1.5s. Skips on pointerdown/touchstart/wheel/keydown/scroll. Test in a fresh browser context (sessionStorage hides it on reload).
- Placeholders use `<span class="todo">TODO</span>` (dashed outline). Never invent work area, KvK, hours, reviews or photos.

## Never

Stock photos/clip-art, pop-ups, forms, chat widgets, service cards with icons, numbered/all-caps section labels,
one italic/coloured word in a headline, prices or discount language, invented facts. (Full list: design doc §9.)

## Checking changes

Screenshot at 390, 768 and 1440px with Playwright and check against the design doc §10:
h1 ≤ 7 words, paragraphs ≤ 3 lines on desktop, links work, visible focus, WCAG AA, no horizontal scroll.

## Open / in progress

- TODO: werkgebied (contact section), KvK number (footer), Work section with 4–6 real photos in `/images` (ready-made markup is in the HTML comment in `<main>`; uncomment and fill in alt texts).
- Open questions for Edward: design doc §11 (work area, KvK, photos, spelling "De-Lina", WhatsApp yes/no).
- Not yet hosted anywhere.
