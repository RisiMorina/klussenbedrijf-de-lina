# Klussenbedrijf De-Lina — website design document

Build a one-page website from this file. Read the whole file before writing code.
Build it as a single `index.html` (CSS and JS inline). All site copy is Dutch.

---

## 1. The business (only what the flyer states)

- **Name:** Klussenbedrijf De-Lina
- **Owner:** Edward. Works alone ("ik"), a few years of experience.
- **Tagline on flyer:** "Kwaliteit voor betaalbare prijs"
- **Services:**
  - Schilderwerk, binnen en buiten
  - Verven en sauzen
  - Tapijt leggen, ook op trappen
  - Stucwerk
  - Laminaatvloeren
- **Selling points he makes himself:** top-quality materials so the work lasts for years; always works something out with clients on price; **no travel costs and no travel hours**.
- **Contact:** Tel 06 42 92 02 03 · E-mail hayk23@hotmail.nl
- **Address:** P.C. Hooftlaan 58, 7412 PT Deventer (shown in the contact section with an embedded Google Map and an "Open in Google Maps" link).
- **Unknown:** work area, KvK number, opening hours, photos of his work. Do not invent any of these. Leave clearly marked TODO placeholders.

## 2. What the site is for

A homeowner or small business owner needs a painter or handyman and wants to know in 10 seconds: what does he do, can I trust him, how do I reach him. The site exists to make them **call Edward**. Nothing else.

- **One action, repeated:** "Bel Edward" (`tel:+31642920203`). In the nav, in the hero, after the services, and at the end. Secondary: e-mail link. On mobile, a WhatsApp link (`https://wa.me/31642920203`) next to the call button is allowed.
- No forms, no quote calculator, no newsletter, no pop-ups.

## 3. Text: reading is opt-in

- Hero: one headline (max ~7 words) and one short line under it. That's all.
- Every other section: one heading plus at most two short sentences.
- No paragraph longer than three lines on desktop.
- Write as Edward talking: "ik", plain words, friendly, not salesy. Correct Dutch spelling (the flyer has errors; don't copy them).

## 4. Sections (in order)

```
┌──────────────────────────────────────────┐
│ De-Lina                      Bel Edward  │  slim bar, hides on scroll down
├──────────────────────────────────────────┤
│                                          │
│  Schilderwerk, stucwerk                  │  HERO
│  en vloeren. Netjes gedaan.              │  big headline, left aligned
│                                          │
│  Binnen en buiten. Geen reiskosten.      │
│  [ Bel Edward ]  of mail                 │
│                                          │
├──────────────────────────────────────────┤
│  Wat ik doe                              │  SERVICES
│  Schilderwerk   ─ binnen en buiten       │  a plain list, not cards
│  Verven en sauzen                        │
│  Stucwerk                                │
│  Tapijt         ─ ook trappen            │
│  Laminaat                                │
├──────────────────────────────────────────┤
│  [ photo of finished work ]              │  WORK (only if photos exist)
├──────────────────────────────────────────┤
│  Eerlijke prijs                          │  PRICE / TRUST
│  Geen reiskosten, geen reisuren.         │
│  We komen er samen altijd uit.           │
├──────────────────────────────────────────┤
│  Even kennismaken?                       │  CONTACT
│  06 42 92 02 03   (huge, tappable)       │
│  hayk23@hotmail.nl                       │
│  Werkgebied: TODO                        │
└──────────────────────────────────────────┘
```

**Added later (Oct 2026), between services and contact, all built from the facts above only:**
- **Zo werk ik:** four steps: U belt of appt → Ik kom kijken → U hoort wat het kost → Ik ga aan de slag. Each step number sits on a small scrap of tape.
- **Eerlijke prijs** gets four short points under the lead: Geen reiskosten, Vooraf duidelijk, Goed materiaal, Eén vakman.
- **Goed om te weten:** a short FAQ in collapsed `<details>` (reading stays opt-in). Never answer with facts we don't have (hours, area, guarantees).
- **Hero note (wide screens):** a paper note "taped to the wall" next to the sub line, with four ticks (services, no travel costs, one tradesman) and the phone number.
- **Tape band:** one long strip of tape across the page between hero and services with the services written on it; slow marquee (static with reduced motion).
- **Layout:** services, price and FAQ get a two-column layout on wide screens (heading sticky on the left). Contact gets address / reachability / work area next to the map.
- **Statement band:** after "Zo werk ik", a dark (`--ink`) band with Edward's own slogan as a big quote ("Kwaliteit voor een betaalbare prijs. Met goed materiaal, zodat u er jaren plezier van hebt."); the words light up one by one while scrolling.
- **Texture:** a very fine plaster grain on the `--plaster` ground; the `--wall` contact band stays smooth like fresh paint. The footer ends with a huge, quiet "De-Lina" wordmark in `--wall`.
- **Footer:** three columns: name + tagline ("Kwaliteit voor een betaalbare prijs"), contact (phone, e-mail, WhatsApp, address), services.

### Copy (use this, adjust lightly if it doesn't fit)

- **Hero headline:** "Schilderwerk, stucwerk en vloeren. Netjes gedaan."
- **Hero line:** "Binnen en buiten. Geen reiskosten, geen reisuren."
- **Services heading:** "Wat ik doe"
- **Services intro (optional):** "Van een kamer sauzen tot een nieuwe vloer. Ik werk met goed materiaal, zodat u er jaren plezier van hebt."
- **Price heading:** "Eerlijke prijs"
- **Price text:** "U betaalt geen reiskosten en geen reisuren. Over de prijs komen we samen altijd uit."
- **Contact heading:** "Even kennismaken?"
- **Contact text:** "Bel of app gerust. Ik kom langs, kijk wat er moet gebeuren en vertel u eerlijk wat het kost."
- **Footer:** "Klussenbedrijf De-Lina · Edward · KvK TODO"

## 5. Photos

- **There are no photos yet.** Real photos of Edward's finished work (a freshly painted room, smooth stucwerk, a carpeted staircase) are what will make this site convincing. Ask for 4–6.
- Until they exist: **leave the Work section out entirely.** Do not use stock photos. Do not use the cartoon painter from the flyer.
- When photos arrive: put them in `/images`, show them full-width, one per screen on mobile, cropped landscape with consistent tone. Before/after pairs are welcome.
- Without photos the page must still never feel empty: the typography and the painter's-tape element (section 7) carry it.

## 6. Look

**Grounded in the trade:** plaster walls, primer, masking tape, a freshly painted wall.

| Token | Hex | Use |
|---|---|---|
| `--plaster` | `#E6E4DF` | page background (cool fresh-plaster grey, not cream) |
| `--wall` | `#FAFAF8` | contact section / alternate band |
| `--ink` | `#1F2328` | text |
| `--muted` | `#5B6168` | secondary text |
| `--tape` | `#2F6DB5` | painter's-tape blue: the only accent. Buttons, the tape strip, links. (Oct 2026: mocha and dark red were tried; blue was chosen as the best.) |
| `--tape-dark` | `#24578F` | button hover / focus; text links (`--tape` on plaster is 4.1:1, fails AA) |
| `--line` | `rgb(31 35 40 / .18)` | service list dividers |
| `--line-soft` | `rgb(31 35 40 / .1)` | nav and mobile call bar borders |

Size tokens: `--text-lead: clamp(1.125rem, 1.6vw, 1.375rem)` for the hero line and every sentence under a heading; `--btn-h: 3.5rem` for all in-page buttons (the nav button stays 2.5rem).

- Never more colour than this. No gradients, no shadows under everything, no rounded cards.
- **Type:** headings in **Archivo** (Google Fonts), weight 800, slightly condensed width (`font-stretch: 85%`), tight leading. Body in **Public Sans** 400/600. Fallback: `system-ui, sans-serif`.
- Big type: hero headline `clamp(2.6rem, 8vw, 6rem)`. Phone number in the contact section just as big.
- Left aligned throughout. Max text width ~60ch.
- Buttons: solid `--tape` rectangle, white text, small radius (3px), label "Bel Edward". No arrows in button text.

## 7. The one memorable thing: painter's tape

Spend all boldness here; keep everything else quiet.

- Each section heading has a strip of blue painter's tape (a slightly rough-edged `--tape` rectangle, a little skewed, ~1–2°) partly behind or under it, like tape on a wall before painting.
- ~~In the hero, a strip of tape peels away on load~~ (replaced, see intro below). The heading tape is static.
- **Intro (the one bold moment):** one wide `--tape` brush stroke paints diagonally (bottom-left → top-right) across a `--plaster` cover. It is built in SVG (feTurbulence + feDisplacementMap for rough edges and bristle streaks), not video. The stroke is a mask: the page shows through it as it paints, then the opening grows to full screen and the intro is removed.
  - It never blocks first understanding: it runs by itself, headline, sub line and "Bel Edward" are fully readable at ~0.8s, and the intro is gone at ~1.05s. Scrolling (wheel, touch, scroll keys) plays it 3× faster; nothing has to be scrolled through, and the hero is never pinned.
  - Both stroke ends sit beyond the screen corners, so no stroke end, edge or hairline is ever visible; only the stroke and the page.
  - The nav sits above the cover, so "Bel Edward" is visible and clickable throughout. Clicking/tapping the cover, Escape/Enter, or tabbing into the page ends the intro at once.
  - Once per visit: `sessionStorage` key `delina-intro` is set when the intro finishes.
  - All content is in the HTML underneath from the start. The cover only appears once the intro script has set itself up (`html.intro-on`), so a script error never hides the page.
  - No other animation in the hero while the intro runs.
- **Scrolling (calm, Feadship-like, never flashy):**
  - Desktop (mouse/trackpad): Lenis 1.3.26 inertia scrolling, loaded from jsDelivr with an integrity hash. Touch devices keep native scrolling.
  - Section headings reveal line by line (each line slides up from behind a mask and fades in); the heading tape then draws in from the left.
  - Short text and the service rows fade in with a slight upward drift, one after another in reading order (110ms apart, never more than 550ms of waiting).
  - Hero: the text block drifts down at 22% of the scroll speed and the headline and sub line fade to 45%, so the next section takes over.
  - Work photos (once they exist) drift inside their frame (`[data-parallax]`); CSS and markup are ready in `index.html`.
  - Only `transform` and `opacity` are animated. Nothing bounces, spins or slides in from the side.
  - "Bel Edward" buttons, the phone number, the nav and the call bar are never part of the scroll animations: never faded, delayed or covered.
  - Everything is in the HTML and readable without JavaScript; motion only runs when JS adds `html.motion`.
- Respect `prefers-reduced-motion`: no intro, no smooth scrolling, no scroll animations, everything simply visible.

## 8. Navigation

- Slim top bar: tape-scrap mark + "De-Lina" + "Klussenbedrijf" on the left, "Bel Edward" button on the right; the phone number as text from tablet width; an anchor menu (Diensten, Werkwijze, Prijs, Vragen, Contact) on wide screens, with the current section underlined in tape.
- Always visible (changed Oct 2026 at the client's request; it used to hide on scroll down).
- On mobile: also a fixed "Bel Edward" button at the bottom of the screen once the hero is scrolled past (respect `env(safe-area-inset-bottom)`).

## 9. Never do this

- Stock photos or clip-art (including the flyer's cartoon man)
- Pop-ups, cookie walls, chat widgets
- Cards in a grid with icons for each service
- Numbered section labels ("01 / Diensten") or tracked-out all-caps labels above headings
- One word in a headline set in italic or a different colour
- Walls of text, or copying the flyer's long paragraphs
- Invented facts: no fake reviews, no "10+ jaar ervaring", no made-up work area, no fake KvK number
- Prices or discount language ("goedkoopste", "actie")

## 10. Quality checks before you finish

- Works and looks intentional at 390px, 768px and 1440px. Take Playwright screenshots at all three and check them against this file.
- Every `tel:` and `mailto:` link works.
- Visible keyboard focus on all links and buttons; colour contrast passes WCAG AA.
- `<title>`: "Klussenbedrijf De-Lina — schilderwerk, stucwerk en vloeren". Add a meta description in Dutch.
- `<html lang="nl">`.
- List every TODO left in the page at the end of your reply.

## 11. Open questions for Edward (not for Claude Code)

- Which area does he work in (city / radius)?
- KvK number?
- Can he send 4–6 photos of finished jobs?
- Is "De-Lina" spelled exactly like that?
- Does he want WhatsApp as a contact option?
