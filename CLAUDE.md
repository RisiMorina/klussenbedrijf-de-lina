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
images/logo.png    Edward's logo (supplied by the client, Oct 2026): transparent cut-out, navy #0F2E48, 522×522
images/logo-192.png, images/apple-touch-icon.png   favicon / home-screen icon (the latter on an opaque plaster ground)
edward-de-lina.vcf contact card behind "Zet Edward in uw contacten" (known facts only; keep in sync with the page)
```

When the site is hosted or sent, `images/` and `edward-de-lina.vcf` must go along with `index.html`.

Logo use (deliberately limited): nav (`.logo-img`, 46px, next to "De-Lina | Klussenbedrijf"), the hero `.memo` header, the footer (`.foot-logo`, 96px, on a plaster disc so the wordmark doesn't show through its open middle), favicon. Don't add it elsewhere, and never on the dark `--ink` band (navy on ink disappears).

Open `index.html` directly in a browser. No dependencies except Google Fonts (Archivo wdth 85 / 800, Public Sans 400/600).

## Page structure (in order)

1. `header.nav`: always visible (never hides; border appears once scrolled, `.is-scrolled`). Logo lockup (`.logo-img` + "De-Lina" + "Klussenbedrijf"; `--nav-h` is 4.25rem to fit it), `.nav-links` anchor menu ≥1180px (active section underlined via IntersectionObserver), "Bel Edward" (>640px only). Section ids: `#diensten #werkwijze #prijs #vragen #contact #locatie` (`#locatie` = the address + map block inside contact; the menu underlines the last matching id in page order).
0. `div.intro` (first in `<body>`): SVG brush-stroke intro overlay + its inline script. Head script adds `html.has-intro` (not yet shown this session, no reduced motion); the intro script adds `html.intro-on` once set up, which shows the cover. Removed from the DOM when finished or skipped.
2. `section.hero` (`.wrap.hero-grid`): h1 (6 words), sub line, `.actions`; ≥1000px also `aside.memo`, a note "taped to the wall" with 4 key facts + phone. No animation in the hero.
2b. `div.band`: decorative (`aria-hidden`) rotated tape strip with the services, slow marquee under `html.motion`. `main` has `overflow-x: clip` for it.
3. `section.services`: "Wat ik doe", `.lead`, plain `ul.list` (not cards).
   Services, price and FAQ use `.layout` (≥1000px: sticky `.side` with h2 + lead on the left, `.main` content on the right).
4. (Work section deliberately absent until real photos exist; see HTML comment TODO.)
4b. `section.how`: "Zo werk ik", `ol.steps` of 4 (number on a `.num` tape scrap, h3, one short line).
4c. `section.statement` (`--ink` band, plaster text): Edward's flyer slogan as a big quote (`#quote`); under motion JS splits it into `.w` word spans (aria-hidden, plus an `.sr` copy) that light up 0.22→1 opacity as it scrolls from 85% to 35% of the viewport.
5. `section.price`: "Eerlijke prijs", lead + `ul.points` (4 trust points, 2 columns ≥768px).
5b. `section.faq`: "Goed om te weten", side has "Staat uw vraag er niet bij?" + a "Neem contact op" link to `#contact`; `<details>` Q&A (opt-in reading; answers only from known facts, no `tel:` inside).
   Plaster sections that follow another plaster section get `.follows` (no top padding).
6. `section.contact` (`--wall` band): lead, large `.phone` number (must stay visible as text for desktop users), Bel Edward + e-mail row, then `.contact-grid`: `dl.facts` (Adres + "Open in Google Maps", Bereikbaar via, Werkgebied TODO) next to `.map` (lazy Google Maps iframe embed, no API key).
7. `footer`: `.foot` grid (logo + flyer tagline, contact incl. address, services), then `.legal` row: © year (JS) + KvK TODO, "Naar boven"; `.wordmark` (huge "De-Lina" in `--wall`, aria-hidden) sits absolutely positioned behind the footer text (`z-index: -1`, centred, cropped at the bottom; on phones lifted above the call-bar space).
   Also: `.skip` link (first focusable), `--grain` plaster noise on body/nav/callbar (contact `--wall` band stays smooth), `::selection` in tape, print styles. `ol.steps::before` is a tape line whose `scaleX(var(--p))` is set from scroll (≥1000px).
   Head also has Open Graph tags and `HousePainter` JSON-LD (known facts only).
8. `.callbar`: mobile only (≤640px), fixed bottom Bel Edward + WhatsApp, appears once the hero is scrolled past.

## Conventions

- **All copy is Dutch**, written as Edward ("ik", "u"). Max 2 short sentences per section, no paragraph over 3 lines on desktop.
- **"Bel Edward"** appears only in the nav (hidden ≤640px, where the call bar takes over), hero and contact (+ mobile call bar). Always `tel:+31642920203`.
  The client found it repeated too often (Oct 2026): no extra Bel Edward buttons after services or FAQ (the FAQ side links to `#contact` instead).
  The phone number as visible text appears only in the contact section (big `.phone`) and the footer; not in the nav or hero note.
- E-mail `mailto:hayk23@hotmail.nl?subject=Klus%20via%20de%20website`; WhatsApp `https://wa.me/31642920203?text=Hallo%20Edward%2C%20ik%20heb%20een%20klus%3A%20` (pre-filled so visitors only have to type their job; use these exact URLs everywhere).
- Helpers: contact has `.copy` "Kopieer nummer" (shown by JS on mouse devices only; Clipboard API with execCommand fallback, label confirms "Gekopieerd"); footer `#share` "Deel deze site" (Web Share API, otherwise copies the link). Both are `hidden` until JS shows them.
- Head has a second JSON-LD block (`FAQPage`) mirroring the "Goed om te weten" Q&A: change both together.
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
  - Lenis 1.3.26 (jsDelivr, SRI hash) is injected only on `(hover: hover) and (pointer: fine)`; it's available as `window.lenis`. Anchor offset -92px (nav + breathing room), matching `scroll-padding-top`.
  - Never put `.reveal` on anything containing a `tel:` link or "Bel Edward": those must never be hidden or delayed.
  - Only animate `transform` and `opacity`.
  - `html.ready`: added by the intro's `finish()`, or 120ms after load when there's no intro, with a 2.6s failsafe in the head script. Until then `.logo-img` (turns in from -120°) and the hero `.memo` (drops in, tape strips press on after) are hidden; never gate anything with "Bel Edward" or `tel:` on it.
  - `.memo` tilts with the mouse in the hero (`--rx/--ry`, ±4°, mouse devices ≥1000px).
  - `.band-track` is moved by JS (no CSS animation): ~35px/s by itself, scroll speed adds an eased boost and sets the direction; the loop only runs while the band is on screen.
  - `.wordmark` rises (translateY 45%→0) as the footer scrolls in.
  - Extras: `.btn::before` darker coat rolls in on hover; divider lines of `.list`/`.points`/`.steps` items draw in (`::after` scaleX) with their reveal; `.num` tape scraps are "pressed on" (scale + rotate settle, `--r` holds the final tilt); FAQ answers ease in on open; `.progress` tape strip under the nav shows reading progress; `.phone` gets a tape strip on hover.
  - Browser support: older-browser fallbacks are written before modern values (`overflow: hidden` before `clip`, `vh` before `svh`, longhand `top/right/bottom/left` instead of `inset`). Keep that pattern. Hero is `min-height: min(100svh, 60rem)`, content centred; on phones (≤640px) no min-height, so the services follow right after.
- Intro is time-driven (`DURATION` 1000ms of progress, `FAST` = 3× once the visitor scrolls). Paint 0–.55, opening .04–.60, opening grows to full screen .55–1, then `finish()` removes it.
  Hero is fully readable at ~0.8s; intro gone at ~1.05s. Stroke length = screen diagonal + stroke width + 80px, so its ends are always off-screen; `skip` starts the dash at the screen edge.
  Cover is `z-index: 9` under the nav (10).
  Slow devices (phones): each frame advances progress by at most `MAX_STEP` (1/24 s), so a phone that renders the filter at a few fps still shows every phase instead of jumping to the end; the clock starts on the second rAF (after the cover is painted); `MAX_WALL` 2500ms is a hard stop. On touch/small screens the `feTurbulence` octaves drop to 1 to make each frame cheaper.
  Headless Edge with `--virtual-time-budget` produces very few frames, so the intro looks "stuck" there; that's the test, not the page.
  Exits: click on the cover, Escape/Enter, focus outside the nav. Test in a fresh browser context (sessionStorage hides it after it finished once). For frame captures use Playwright's paused clock (`clock.install` + `pauseAt` + `runFor`), since the intro runs on requestAnimationFrame time.
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
