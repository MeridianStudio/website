# Meridian — Design System & Style Guide

A reference document for all UI development on the Meridian website.
Use this to maintain visual consistency across pages and components.

---

## 1. Design Principles

- **Warm minimalism.** Ample whitespace, restrained decoration, warmth through colour temperature rather than pattern.
- **Editorial confidence.** Typography does the heavy lifting. Headings are large, unhurried, and set in a high-contrast serif.
- **Subtle motion.** Interactions are gentle — slow fades, slight translates, no bouncing or dramatic effects.
- **Luxury without coldness.** The palette avoids the cool greys common in SaaS. Everything leans warm.

---

## 2. Colour Palette

All colours are defined as CSS custom properties on `:root`.

### Core Tokens

| Token            | Hex         | Usage                                              |
|------------------|-------------|-----------------------------------------------------|
| `--cream`        | `#f9f7f4`   | Page background, nav background                    |
| `--warm-white`   | `#ffffff`   | Section backgrounds (services, CTA)                |
| `--ink`          | `#1a1814`   | Primary text, primary button background            |
| `--ink-light`    | `#6b6660`   | Secondary text, nav links, body copy               |
| `--ink-faint`    | `#b5b0aa`   | Tertiary text, timestamps, footnotes, step numbers |
| `--accent`       | `#c17f4a`   | Italic headline colour, section labels, borders, CTAs, dots |
| `--accent-light` | `#e8d5c0`   | Tag borders, hover tints                           |
| `--accent-faint` | `#f5ede4`   | Tag backgrounds, card hover state, radial gradient blob |
| `--border`       | `#e8e4df`   | All dividers, card borders, nav scroll border      |

### Dark Surface

The intro strip uses `--ink` (`#1a1814`) as a full-bleed background with white text at reduced opacity:

- Primary text on dark: `rgba(255, 255, 255, 0.9)`
- Secondary text on dark: `rgba(255, 255, 255, 0.6)`

### Usage Rules

- Never use pure black (`#000`) or pure white (`#fff`) for backgrounds.
- The accent colour (`#c17f4a`) is used for **italic display text, section labels, tags, borders, and interactive elements**. It is never used for body text.
- Buttons invert: primary button is `--ink` background with white text; on hover it shifts to `--accent`.

---

## 3. Typography

### Fonts

```css
--font-display: 'Cormorant Garamond', serif;
--font-body:    'DM Sans', sans-serif;
```

**Cormorant Garamond** — Google Fonts. Used for all display headings, the logo, large pull quotes, the footer tagline, and decorative watermark text. Always set at `font-weight: 300` or `400`; never bold. Italics are used expressively for the second line of split headlines and the footer tagline.

**DM Sans** — Google Fonts. Used for all body copy, nav links, buttons, labels, and tags. The base body weight is `300` (light). UI labels and buttons use `400` (regular).

---

### Type Scale

#### Display / Section Headlines

Split into two lines: a roman (upright) first line and an italic, accent-coloured second line.

```css
.section-title {
  font-family: var(--font-display);
  font-size: clamp(2.2rem, 4vw, 3.8rem);
  font-weight: 300;
  line-height: 1.15;
  max-width: 640px;
}
.section-title em {
  font-style: italic;
  color: var(--accent);
}
```

#### Hero Headline

```css
.hero-headline {
  font-family: var(--font-display);
  font-size: clamp(3.5rem, 6vw, 6rem);
  font-weight: 300;
  line-height: 1.05;
  letter-spacing: -0.01em;
}
.hero-headline em {
  font-style: italic;
  color: var(--accent);
}
```

#### Intro Strip Quote (large italic on dark)

```css
font-family: var(--font-display);
font-size: clamp(1.5rem, 2.5vw, 2.2rem);
font-weight: 300;
font-style: italic;
line-height: 1.4;
color: rgba(255, 255, 255, 0.9);
```

#### Section Label (eyebrow text)

Used above every section heading. All-caps, wide tracking, accent colour.

```css
.section-label {
  font-size: 0.72rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1rem;
}
```

#### Body Copy

```css
font-family: var(--font-body);
font-size: 1.05rem;   /* hero body */
font-size: 0.95rem;   /* general section body */
font-size: 0.88rem;   /* card/step descriptions */
font-weight: 300;
line-height: 1.75–1.8;
color: var(--ink-light);
```

#### Small / Meta Text

```css
font-size: 0.78rem;
color: var(--ink-faint);
```

#### Navigation Logo

```css
.nav-logo {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 400;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink);
}
```

#### Navigation Links

```css
font-family: var(--font-body);
font-size: 0.8rem;
letter-spacing: 0.08em;
text-transform: uppercase;
color: var(--ink-light);
```

#### Button / Tag Text

```css
font-size: 0.8rem;
font-weight: 400;
letter-spacing: 0.1em;
text-transform: uppercase;
```

---

## 4. Spacing System

Spacing is set in `rem` and follows a loose scale. No utility framework — values are hand-placed by context.

| Use                          | Value            |
|------------------------------|------------------|
| Section vertical padding     | `7rem 4rem`      |
| Hero padding                 | `8rem 4rem 6rem` |
| Nav padding                  | `1.5rem 4rem`    |
| Card internal padding        | `3rem 2.5rem`    |
| Process step padding         | `0 2rem`         |
| Intro strip padding          | `4rem`           |
| CTA section padding          | `8rem 4rem`      |
| Hero divider margin          | `2.5rem 0`       |
| Hero actions margin-top      | `3rem`           |
| Section header margin-bottom | `4rem`           |
| Process header margin-bottom | `5rem`           |
| Button padding               | `1rem 2.25rem`   |
| Tag padding                  | `0.3rem 0.75rem` |
| Nav links gap                | `2.5rem`         |
| Hero actions gap             | `2rem`           |

---

## 5. UI Components & Patterns

### Navigation

Fixed, full-width bar. Transparent border-bottom that becomes `--border` on scroll (class `.scrolled` toggled via JS). Background is a semi-transparent cream with `backdrop-filter: blur(12px)`.

- **Logo**: Cormorant Garamond, uppercase, `letter-spacing: 0.12em`
- **Links**: DM Sans, uppercase, small, `--ink-light` → `--ink` on hover
- **CTA button**: Outlined style — `--accent` text and border, transparent background; fills to `--accent` background on hover

```css
.nav-cta {
  font-size: 0.78rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--accent);
  border: 1px solid var(--accent);
  padding: 0.5rem 1.25rem;
  border-radius: 2px;
  transition: background 0.2s, color 0.2s;
}
.nav-cta:hover {
  background: var(--accent);
  color: white;
}
```

---

### Buttons

Two types only:

**Primary** — filled, dark, uppercase

```css
.btn-primary {
  display: inline-block;
  background: var(--ink);
  color: white;
  font-family: var(--font-body);
  font-size: 0.8rem;
  font-weight: 400;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  padding: 1rem 2.25rem;
  border-radius: 2px;
  transition: background 0.25s, transform 0.2s;
}
.btn-primary:hover {
  background: var(--accent);
  transform: translateY(-1px);
}
```

**Secondary** — text link with arrow, uppercase

```css
.btn-secondary {
  font-size: 0.8rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--ink-light);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: color 0.2s, gap 0.2s;
}
.btn-secondary:hover { color: var(--ink); gap: 0.75rem; }
.btn-secondary::after { content: '\2192'; } /* → */
```

---

### Service Tags (pill labels)

Used inside cards to label service types. Outlined, accent colour, faint background fill.

```css
.service-tag {
  display: inline-block;
  font-size: 0.7rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--accent);
  border: 1px solid var(--accent-light);
  background: var(--accent-faint);
  padding: 0.3rem 0.75rem;
  border-radius: 2px;
  white-space: nowrap;
}
```

---

### Hero Section

- Full-viewport height (`min-height: 100vh`)
- Left-aligned content
- Decorative watermark: the letter **"M"** rendered in `--font-display` at `clamp(20rem, 35vw, 42rem)`, positioned absolute to the right, `color: var(--accent-faint)`, `opacity: 0.6`. Generated via CSS `::before` pseudo-element on `.hero`.
- A short horizontal rule divider (`3rem` wide, `1px` tall, `--accent` colour) sits between the headline and body copy.
- Entry animation: all child elements use `fadeUp` keyframe with staggered delays (`0.3s`, `0.4s`, `0.6s`, `0.75s`, `0.9s`).

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

---

### Intro Strip (dark band)

Full-bleed dark section (`--ink` background) that breaks the cream-on-white rhythm. Two-column grid: large italic pull quote on the left, explanatory body paragraph on the right.

```css
.intro-strip {
  background: var(--ink);
  color: white;
  padding: 4rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}
```

---

### Service Cards

Three-column grid with a shared border forming a single outlined container. Each card has a `border-right`; the last card has none. Cards show a `--accent-faint` background on hover.

```css
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  border: 1px solid var(--border);
}
.service-card {
  padding: 3rem 2.5rem;
  border-right: 1px solid var(--border);
  transition: background 0.3s;
}
.service-card:hover { background: var(--accent-faint); }
```

Card anatomy (top to bottom):
1. Large muted number (`01`, `02`, `03`) in Cormorant Garamond, `--ink-faint` colour
2. Card title in body font, regular weight
3. Descriptive body paragraph
4. Service tag label at the bottom

---

### Process Timeline

Four-column grid with a horizontal rule connecting step dots. The rule is generated by a `::before` pseudo-element on the grid container, centred vertically on the dots.

```css
.process-steps {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  position: relative;
}
.process-steps::before {
  content: '';
  position: absolute;
  top: 1.2rem;
  left: calc(100% / 8);
  right: calc(100% / 8);
  height: 1px;
  background: var(--border);
}
.step-dot {
  width: 2.4rem;
  height: 2.4rem;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: var(--cream);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 2rem;
  position: relative;
  z-index: 1;
  transition: border-color 0.3s, background 0.3s;
}
.process-step:hover .step-dot {
  border-color: var(--accent);
  background: var(--accent);
}
.step-dot-inner {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--accent);
}
.process-step:hover .step-dot-inner { background: white; }
```

---

### CTA Section

Centred layout on a white background with a soft radial gradient blob (decorative, non-interactive) behind the content:

```css
.cta-section::before {
  content: '';
  position: absolute;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  width: 600px; height: 600px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--accent-faint) 0%, transparent 70%);
  pointer-events: none;
}
```

The CTA email link uses an underline style (bottom border, not text-decoration) and includes an arrow →.

---

### Footer

Three-column flex layout. All text at `0.78rem` in `--ink-faint`. The tagline is italic Cormorant Garamond. A small `5px` circular accent dot precedes the location text.

```css
footer {
  padding: 2.5rem 4rem;
  border-top: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

---

## 6. Border Radius

Intentionally minimal. The design uses `border-radius: 2px` on all interactive elements (buttons, tags, nav CTA). Circular elements (step dots, location dot) use `border-radius: 50%`. No rounded cards or modals.

---

## 7. Borders & Dividers

All borders use `--border` (`#e8e4df`) at `1px solid`. Dividers are used to:
- Separate the nav from content on scroll
- Frame the services grid
- Separate cards within the services grid
- Top-border the footer
- Connect process steps (via pseudo-element)

---

## 8. Motion & Animation

- **Entry animation**: `fadeUp` — elements fade in while translating up `24px`, over `0.8–0.9s` with `ease` timing. Used for hero elements with staggered delays. Controlled by the `.reveal` class toggled via IntersectionObserver.
- **Hover transitions**: All `0.2–0.3s` duration. Transitions cover `background`, `color`, `transform`, `gap`, `border-color`, `opacity`.
- **Page scroll**: `scroll-behavior: smooth` on `html`.
- **Primary button hover**: `translateY(-1px)`.
- **Secondary button hover**: gap between text and arrow expands from `0.5rem` to `0.75rem`.

---

## 9. Layout

- **Max content width**: Not globally capped; `4rem` horizontal padding acts as the gutter.
- **Grid**: CSS Grid used for multi-column sections. No framework.
  - Services: `repeat(3, 1fr)`
  - Process: `repeat(4, 1fr)`
  - Intro strip: `1fr 1fr`
- **Flexbox**: Used for nav, footer, button groups, and inline elements.
- **Section padding**: Consistent `7rem 4rem` on all `<section>` elements.

---

## 10. Responsive Notes

The design uses `clamp()` for fluid type scaling:

```css
font-size: clamp(3.5rem, 6vw, 6rem);     /* hero headline */
font-size: clamp(2.2rem, 4vw, 3.8rem);   /* section titles */
font-size: clamp(1.5rem, 2.5vw, 2.2rem); /* intro quote */
font-size: clamp(20rem, 35vw, 42rem);    /* watermark letter */
```

No explicit breakpoints are defined in the current file. Mobile layout adaptations should follow the same warm-minimal aesthetic with stacked columns and reduced section padding (`3rem 1.5rem` suggested).

---

## 11. Do's and Don'ts

**Do:**
- Use Cormorant Garamond exclusively for display text; never for body, labels, or UI
- Keep italic + accent colour as a paired effect — they always appear together
- Use `--accent` sparingly: labels, italic text, interactive accents only
- Maintain the warm temperature throughout — no cool greys or blue tones
- Use the `2px` border-radius consistently on all rectangular interactive elements

**Don't:**
- Use bold weights in Cormorant Garamond (it breaks the delicate look)
- Use `--accent` as a background fill for large areas
- Add drop shadows — the design relies on borders and background contrast instead
- Introduce new typefaces or font weights not listed here
- Use decorative icons or emoji — the design is typographic only
