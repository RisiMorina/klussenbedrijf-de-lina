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
privacy.html       privacy page, same look (tokens + nav/footer CSS duplicated inline; keep in sync with index.html). TODOs: hosting, retention
images/og-image.png 1200×630 share image (plaster, logo, name, tagline); og:image in index.html is relative until the site is hosted (TODO: absolute URL)
edward-de-lina.vcf contact card behind "Zet Edward in uw contacten" (known facts only; keep in sync with the page)
```

When the site is hosted or sent, `images/` and `edward-de-lina.vcf` and `privacy.html` must go along with `index.html`.

Logo use (deliberately limited): nav (`.logo-img`, 46px, next to "De-Lina | Klussenbedrijf"), the hero `.memo` header, the footer (`.foot-logo`, 96px, on a plaster disc so the wordmark doesn't show through its open middle), favicon. Don't add it elsewhere, and never on the dark `--ink` band (navy on ink disappears).

Open `index.html` directly in a browser. No dependencies except Google Fonts (Archivo wdth 85 / 800, Public Sans 400/600).

## Page structure (in order)

1. `header.nav`: always visible (never hides; border appears once scrolled, `.is-scrolled`). Logo lockup (`.logo-img` + "De-Lina" + "Klussenbedrijf"; `--nav-h` is 4.25rem to fit it), `.nav-links` anchor menu ≥1180px (active section underlined via IntersectionObserver), "Bel Edward" (>640px only). Menu: Diensten, Prijs, Vragen, Contact (no Werkwijze, no Locatie). Section ids `#diensten #werkwijze #prijs #vragen #contact #locatie` still exist as anchors (`#locatie` = address + map block inside contact; FAQ links to it).
2. `section.hero` (`.wrap.hero-grid`): h1 (6 words), sub line, `.actions`; ≥1000px also `aside.memo`, a note "taped to the wall" with 4 key facts + phone. No animation in the hero.
2b. `div.band`: decorative (`aria-hidden`) rotated tape strip with the services. Static, wraps on narrow screens. `main` has `overflow-x: clip` for it.
3. `section.services`: "Wat ik doe", `.lead`, plain `ul.list` (not cards).
   Services, price and FAQ use `.layout` (≥1000px: sticky `.side` with h2 + lead on the left, `.main` content on the right).
4. (Work section deliberately absent until real photos exist; see HTML comment TODO.)
4b. `section.how`: "Zo werk ik", `ol.steps` of 4 (number on a `.num` tape scrap, h3, one short line).
4c. `section.statement` (`--ink` band, plaster text): Edward's flyer slogan as a big quote (`#quote`). Static.
5. `section.price`: "Eerlijke prijs", lead + `ul.points` (4 trust points, 2 columns ≥768px).
5b. `section.faq`: "Goed om te weten", side has "Staat uw vraag er niet bij?" + a "Neem contact op" link to `#contact`; `<details>` Q&A (opt-in reading; answers only from known facts, no `tel:` inside).
   Plaster sections that follow another plaster section get `.follows` (no top padding).
6. `section.contact` (`--wall` band): lead, large `.phone` number (must stay visible as text for desktop users), Bel Edward + e-mail row, then `.contact-grid`: `dl.facts` (Adres + "Open in Google Maps", Bereikbaar via, Werkgebied TODO) next to `.map` (lazy Google Maps iframe embed, no API key).
7. `footer`: `.foot` grid (logo + flyer tagline, contact incl. address, services), then `.legal` row: © year (JS) + KvK TODO, "Deel deze site", "Privacy" (→ `privacy.html`), "Naar boven"; `.wordmark` (huge "De-Lina" in `--wall`, aria-hidden) sits absolutely positioned behind the footer text (`z-index: -1`, centred, cropped at the bottom; on phones lifted above the call-bar space).
   Also: `.skip` link (first focusable), `--grain` plaster noise on body/nav/callbar (contact `--wall` band stays smooth), `::selection` in tape, print styles.
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
- **Motion is deliberately minimal (client wanted less, Oct 2026).** The brush-stroke intro was removed (Oct 2026). Only one thing moves: the tape under each h2, which draws in once (`h2.in .taped::before` scaleX 0→1) via an IntersectionObserver, only under `html.motion` (head script: JS on, no reduced motion). Without it everything is static and visible. Removed on purpose, don't bring back: reveals, h2 line splitting, hero parallax/fade, Lenis, marquee, word-lighting quote, memo tilt/drop-in, logo spin, wordmark rise, reading bar, button paint effect, drawing divider lines, steps tape line, FAQ ease-in, smooth anchor scrolling. Hover states (nav underline, service and phone tape) stay.
  - Only animate `transform` and `opacity`.
  - Browser support: older-browser fallbacks are written before modern values (`overflow: hidden` before `clip`, `vh` before `svh`, longhand `top/right/bottom/left` instead of `inset`). Keep that pattern. Hero is `min-height: min(100svh, 60rem)`, content centred; on phones (≤640px) no min-height, so the services follow right after.
- Placeholders use `<span class="todo">TODO</span>` (dashed outline). Never invent work area, KvK, hours, reviews or photos.

## Never

Stock photos/clip-art, pop-ups, forms, chat widgets, service cards with icons, numbered/all-caps section labels,
one italic/coloured word in a headline, prices or discount language, invented facts. (Full list: design doc §9.)

## Checking changes

Screenshot at 390, 768 and 1440px with Playwright and check against the design doc §10:
h1 ≤ 7 words, paragraphs ≤ 3 lines on desktop, links work, visible focus, WCAG AA, no horizontal scroll.

## Open / in progress

- TODO: werkgebied (contact section), KvK number (footer and privacy page), hosting and retention (privacy page), absolute og:image URL once hosted, Work section with 4–6 real photos in `/images` (ready-made markup is in the HTML comment in `<main>`; uncomment and fill in alt texts).
- Open questions for Edward: design doc §11 (work area, KvK, photos, spelling "De-Lina", WhatsApp yes/no, is P.C. Hooftlaan 58 a home address, may "Ik kom kijken" / "vooraf duidelijk wat het kost" stay).
- Not yet hosted anywhere.
