# Gravitonic Design Language — Complete Guide

> Apply the same design system from your Gravitonic landing page to any new website. This document covers every design decision — colors, typography, spacing, components, motion, and responsive behavior.

---

## Table of Contents

1. [Design Philosophy](#1-design-philosophy)
2. [Color System](#2-color-system)
3. [Typography](#3-typography)
4. [Spatial System](#4-spatial-system)
5. [Components](#5-components)
6. [Motion & Animation](#6-motion--animation)
7. [Shadows & Borders](#7-shadows--borders)
8. [Dark Sections](#8-dark-sections)
9. [Responsive Breakpoints](#9-responsive-breakpoints)
10. [CSS Variables Reference](#10-css-variables-reference)
11. [Component Patterns](#11-component-patterns)
12. [Quick Start Template](#12-quick-start-template)
13. [Apply Checklist](#13-apply-checklist)

---

## 1. Design Philosophy

Your design is built on **restraint and clarity**. The system uses minimal colors, generous whitespace, subtle borders, and a consistent rounded aesthetic to feel premium without being loud.

### Core Principles

| Principle | Implementation |
|---|---|
| **Quiet luxury** | White background, muted text, no heavy gradients, subtle borders |
| **Consistent radius** | Every card/button uses the same `9999px` (full pill) for buttons, `24px` for cards |
| **Transparency over depth** | Cards use `rgba()` backgrounds at ~5% opacity instead of drop shadows |
| **One accent color** | Black (`#121317`) is the primary accent — not blue or purple |
| **Fixed max-width** | `1744px` container with `72px` side padding (desktop) |
| **Subtle reveal** | Header hides on scroll-down, reappears on scroll-up |

---

## 2. Color System

### CSS Variables (copy this block into every project)

```css
:root {
    /* === Core Palette === */
    --ag-black: #121317;
    --ag-white: #ffffff;
    --ag-gray-muted: #45474d;
    --ag-gray-light: rgba(183, 191, 217, 0.1);
    --ag-gray-border: rgba(33, 34, 38, 0.06);

    /* === Card Surfaces === */
    --card-bg: rgba(183, 191, 217, 0.05);
    --icon-badge-bg: rgba(183, 191, 217, 0.09);
}
```

### Color Usage Map

| Variable | Usage |
|---|---|
| `--ag-black` | Text, buttons (primary), icon strokes, borders |
| `--ag-white` | Background, inverse button text |
| `--ag-gray-muted` | Secondary text, captions, placeholders |
| `--ag-gray-light` | Secondary button backgrounds |
| `--ag-gray-border` | Card borders (1px, ultra-subtle) |
| `--card-bg` | Card surfaces |
| `--icon-badge-bg` | Circular icon containers |

### Why This Works

- **Grayscale base** — no hue pollution. You can swap the single accent (`--ag-black`) to any color and the whole system changes.
- **Single value** for all borders: `0.8px solid var(--ag-gray-border)` — same across every element.
- **Transparent tints** — `rgba(183, 191, 217, 0.05)` creates depth without shadow. On dark sections, just invert.
- **One-number tint system** — `rgba(183, 191, 217, X)` where X scales: `0.05` for cards, `0.09` for icon badges, `0.1` for secondary buttons, `0.2` for inverse elements.

### Adapting for Dark Mode

```css
[data-theme="dark"] {
    --ag-black: #ffffff;
    --ag-white: #0d0f14;
    --ag-gray-muted: rgba(255, 255, 255, 0.6);
    --ag-gray-border: rgba(255, 255, 255, 0.06);
    --card-bg: rgba(255, 255, 255, 0.05);
    --icon-badge-bg: rgba(255, 255, 255, 0.09);
}
```

---

## 3. Typography

### Font Stack

```html
<link href="https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;450;500&display=swap" rel="stylesheet">
```

```css
body {
    font-family: "Google Sans Flex", "Google Sans", sans-serif;
    line-height: 24px;
    -webkit-font-smoothing: antialiased;
}
```

### Type Scale

| Element | Size | Weight | Line Height | Letter Spacing |
|---|---|---|---|---|
| Body | 16px | 400 | 24px | 0 |
| Nav links | 14.5px | 450 | 21px | 0.11px |
| Button text | 17.5px | 450 | 25px | 0.18px |
| Section heading (h2) | 54px | 450 | 56px | -0.95px |
| Hero heading (h1) | 80px | 450 | 88px | 0 |
| Card title (h3) | 24px | 450 | 1.2em | 0 |
| Card body | 15px | 400 | 1.5em | 0 |
| Footer text | 14px | 400 | 1.5em | 0 |
| Stat number | 64px | 450 | 1 | 0 |
| Blog title | 20px | 450 | 1.2em | 0 |

### Key Typographic Rules

1. **Font weight 450** (not 400 or 500) — the sweet spot that feels premium and readable.
2. **Tight letter-spacing on large headings**: `-0.95px` on section headings (`54px`) creates a modern, confident feel.
3. **No decorative fonts** — pure geometric sans throughout. Every text element uses the same font.
4. **Line-height 24px** for body text — slightly relaxed (1.5x font size of 16px).
5. **Always include `-webkit-font-smoothing: antialiased`** — keeps text crisp on all screens.

---

## 4. Spatial System

### Container

```css
.container {
    max-width: 1744px;
    margin: 0 auto;
    padding: 0 72px;
}
```

| Breakpoint | Padding |
|---|---|
| Desktop (>1200px) | `72px` |
| Tablet (768–1200px) | `40px` |
| Mobile (<768px) | `24px` |

### Section Spacing

```css
section {
    padding: 120px 0;  /* Desktop */
}

@media (max-width: 768px) {
    section {
        padding: 80px 0;
    }
}
```

### Grid System

**3-column grid** (services, testimonials, blog):
```css
.grid-3 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
}
```

**2-column grid** (features):
```css
.grid-2 {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
}
```

**4-column grid** (stats):
```css
.stats-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 48px;
}
```

All grids collapse to `1fr` on mobile.

### Spacing Scale

| Token | Value | Usage |
|---|---|---|
| `--space-xs` | 8px | Tight gaps |
| `--space-sm` | 12px | Icon-label spacing |
| `--space-md` | 16px | Default gap |
| `--space-lg` | 24px | Card padding, section gaps |
| `--space-xl` | 32px | Inner card padding |
| `--space-2xl` | 48px | Grid gaps, section margins |
| `--space-3xl` | 64px | Section dividers, section header margin |
| `--space-4xl` | 80px | Section padding top/bottom, footer padding |

---

## 5. Components

### 5.1 Header / Navigation Bar

**Visual specs:**
- Height: `52px` fixed
- Background: `rgba(255, 255, 255, 0.95)`
- Backdrop blur: `12px`
- Bottom border: `0.8px solid var(--ag-gray-border)`
- z-index: `1000`

**Behavior:**
- Hides on scroll-down when past 100px
- Reappears on scroll-up
- Transition: `transform 0.3s ease-in-out`

```css
header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 52px;
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    z-index: 1000;
    border-bottom: 0.8px solid var(--ag-gray-border);
    transition: transform 0.3s ease-in-out;
}

header.hidden {
    transform: translateY(-100%);
}

.header-inner {
    max-width: 1744px;
    margin: 0 auto;
    padding: 0 72px;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
```

**Nav link hover** — use opacity, not underline:
```css
nav a {
    font-size: 14.5px;
    font-weight: 450;
    letter-spacing: 0.11px;
    color: var(--ag-black);
    text-decoration: none;
    transition: opacity 0.15s ease-out;
}

nav a:hover {
    opacity: 0.7;
}
```

**Logo size**: `162px` width, `auto` height.

---

### 5.2 Buttons

**4 button variants** — all pill-shaped with `border-radius: 9999px`:

```css
.btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 10px 24px;
    border-radius: 9999px;
    font-size: 17.5px;
    font-weight: 450;
    letter-spacing: 0.18px;
    line-height: 25.38px;
    text-decoration: none;
    border: none;
    cursor: pointer;
    transition: all 0.15s ease-out;
}
```

| Variant | Class | Background | Color | Border |
|---|---|---|---|---|
| **Primary** | `btn-primary` | `--ag-black` | `--ag-white` | none |
| **Primary Inverse** | `btn-primary-inverse` | `--ag-white` | `--ag-black` | none |
| **Secondary** | `btn-secondary` | `--ag-gray-light` | `--ag-black` | `0.8px solid --ag-gray-border` |
| **Secondary Inverse** | `btn-secondary-inverse` | `rgba(183, 191, 217, 0.2)` | `--ag-white` | `0.8px solid rgba(230, 234, 240, 0.06)` |

**All button hover states:**
```css
.btn-primary:hover,
.btn-secondary:hover { opacity: 0.85; }

.btn-primary-inverse:hover,
.btn-secondary-inverse:hover { opacity: 0.9; }
```

No color change on hover. No transform. Just a subtle fade — this keeps the interaction vocabulary clean.

> **Rule**: Use inverse button variants (`-inverse`) only inside dark (`--ag-black` background) sections. Use primary variants on light sections.

---

### 5.3 Cards

**Service / Testimonial / Blog Cards** — uniform style:

```css
.card {
    background: var(--card-bg);
    border: 0.8px solid var(--ag-gray-border);
    border-radius: 24px;
    padding: 32px;
}
```

**Card hover effect** — `translateY(-4px)` only. No shadow, no color shift:
```css
.card:hover {
    transform: translateY(-4px);
}
```

**Card anatomy**:
```
┌─────────────────────────────┐
│  [icon-badge]               │  ← icon-badge (98px circle) or image
│                             │
│  Title (h3, 24px, 450)      │
│  Description text (15px)    │
│                             │
│  [optional CTA button]      │
└─────────────────────────────┘
```

---

### 5.4 Icon Badges

Circular container for service icons:

```css
.icon-badge {
    width: 98px;
    height: 98px;
    border-radius: 50%;
    background: var(--icon-badge-bg);  /* rgba(183, 191, 217, 0.09) */
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 24px;
}

.icon-badge svg {
    width: 40px;
    height: 40px;
    stroke: var(--ag-black);           /* #121317 */
    stroke-width: 2;
    fill: none;
}
```

All SVG icons: line-based (no fill), `stroke="#121317"`, `stroke-width="2"`. Clean, minimal, consistent.

---

### 5.5 Section Headers

Every section uses the same centered header pattern:

```css
.section-header {
    text-align: center;
    margin-bottom: 64px;
}

.section-header h2 {
    font-size: 54px;
    font-weight: 450;
    line-height: 56.16px;
    letter-spacing: -0.95px;
    margin-bottom: 16px;
}

.section-header p {
    color: var(--ag-gray-muted);
    max-width: 600px;
    margin: 0 auto;
}
```

---

### 5.6 Footer

**Footer grid** (4 columns, brand gets 2x width):

```css
.footer-grid {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 48px;
    margin-bottom: 64px;
}
```

**Footer styling**:
- Background: `--ag-black`
- Link color: `rgba(255, 255, 255, 0.6)`
- Hover: `color: var(--ag-white)`
- Copyright: `rgba(255, 255, 255, 0.4)`
- Bottom border: `0.8px solid rgba(255, 255, 255, 0.1)`
- Social icons: SVG, `20×20px`, no background circle

---

## 6. Motion & Animation

### Header Scroll Behavior

```javascript
let lastScroll = 0;
const header = document.getElementById('header');

window.addEventListener('scroll', () => {
    const currentScroll = window.pageYOffset;

    if (currentScroll > lastScroll && currentScroll > 100) {
        header.classList.add('hidden');
    } else {
        header.classList.remove('hidden');
    }

    lastScroll = currentScroll;
});
```

**Logic**: hide when scrolling down past 100px, show when scrolling up.

### Typed Text Animation

```javascript
const phrases = ['Orbit', 'Tomorrow', 'Success', 'Growth'];
let phraseIndex = 0;
let charIndex = 0;
let isDeleting = false;
const typedElement = document.getElementById('typed');

function type() {
    const currentPhrase = phrases[phraseIndex];

    if (isDeleting) {
        typedElement.textContent = currentPhrase.substring(0, charIndex - 1);
        charIndex--;
    } else {
        typedElement.textContent = currentPhrase.substring(0, charIndex + 1);
        charIndex++;
    }

    let typeSpeed = isDeleting ? 30 : 40;

    if (!isDeleting && charIndex === currentPhrase.length) {
        typeSpeed = 2000;
        isDeleting = true;
    } else if (isDeleting && charIndex === 0) {
        isDeleting = false;
        phraseIndex = (phraseIndex + 1) % phrases.length;
        typeSpeed = 500;
    }

    setTimeout(type, typeSpeed);
}

type();
```

**Timing pattern**: type 40ms/char → pause 2000ms → delete 30ms/char → pause 500ms → next phrase.

### CSS Transitions Summary

| Element | Property | Duration | Easing |
|---|---|---|---|
| Nav links | `opacity` | `0.15s` | `ease-out` |
| Buttons | `all` | `0.15s` | `ease-out` |
| Cards | `transform` | `0.15s` | `ease-out` |
| Footer links | `color` | `0.15s` | `ease-out` |
| Header | `transform` | `0.3s` | `ease-in-out` |
| Cursor blink | `opacity` | `0.8s` | `infinite` |

**Rule**: All transitions use `ease-out` except the header which uses `ease-in-out` for a smoother feel.

---

## 7. Shadows & Borders

### The "No Shadow" Rule

This design **never uses box-shadow**. Depth is achieved through:

1. **Transparent backgrounds** — `rgba(183, 191, 217, 0.05)` creates a subtle raised surface
2. **Borders** — `0.8px solid var(--ag-gray-border)` defines edges cleanly
3. **Hover lift** — `translateY(-4px)` gives tactile feedback

### Border System — Single Value

Every border in the design uses the same value:

```css
border: 0.8px solid var(--ag-gray-border);
/* rgba(33, 34, 38, 0.06) — barely visible on white */
```

Applied to:
- Header bottom border
- All cards (service, feature, testimonial, blog)
- Secondary buttons
- Footer bottom separator

---

## 8. Dark Sections

Dark sections use **color inversion**, not a new palette. The CSS variables flip their roles — `--ag-black` becomes the background, `--ag-white` becomes text.

```css
.stats-section,
.cta-section {
    background: var(--ag-black);
    color: var(--ag-white);
}
```

**Stats section**:
- Full `--ag-black` background
- Large stat numbers: `64px`, `font-weight: 450`, `line-height: 1`
- Labels: `rgba(255, 255, 255, 0.7)` — muted white
- 4-column grid with `48px` gap

**CTA section**:
- Full `--ag-black` background
- Centered text, max-width `600px`
- `h2` at `54px` with `letter-spacing: -0.95px`
- Inverse buttons (`btn-primary-inverse`, `btn-secondary-inverse`)
- Paragraph: `rgba(255, 255, 255, 0.7)`

---

## 9. Responsive Breakpoints

```css
/* Tablet — 768px to 1200px */
@media (max-width: 1200px) {
    .container { padding: 0 40px; }

    .services-grid,
    .testimonials-grid,
    .blog-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 32px;
    }
}

/* Mobile — below 768px */
@media (max-width: 768px) {
    .container { padding: 0 24px; }
    section { padding: 80px 0; }

    .hero h1 {
        font-size: 48px;
        line-height: 56px;
    }

    .section-header h2 {
        font-size: 36px;
        line-height: 44px;
    }

    .services-grid,
    .features-grid,
    .testimonials-grid,
    .blog-grid {
        grid-template-columns: 1fr;
    }

    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .footer-grid {
        grid-template-columns: 1fr 1fr;
    }

    nav { display: none; }  /* Replace with hamburger menu */
}
```

**Rules**:
- All multi-column grids collapse to single column on mobile
- Typography scales down ~40%
- Nav becomes hamburger menu on mobile
- Footer grid: 4 columns → 2 columns

---

## 10. CSS Variables Reference

**Full block — copy this into every new project:**

```css
:root {
    /* === COLORS === */
    --ag-black: #121317;
    --ag-white: #ffffff;
    --ag-gray-muted: #45474d;
    --ag-gray-light: rgba(183, 191, 217, 0.1);
    --ag-gray-border: rgba(33, 34, 38, 0.06);
    --card-bg: rgba(183, 191, 217, 0.05);
    --icon-badge-bg: rgba(183, 191, 217, 0.09);

    /* === SPACING === */
    --space-xs: 8px;
    --space-sm: 12px;
    --space-md: 16px;
    --space-lg: 24px;
    --space-xl: 32px;
    --space-2xl: 48px;
    --space-3xl: 64px;
    --space-4xl: 80px;

    /* === LAYOUT === */
    --container-max: 1744px;
    --container-padding: 72px;
    --border-radius-card: 24px;
    --border-radius-pill: 9999px;
}
```

---

## 11. Component Patterns

### Pattern 1: Section with centered header + 3-column grid

```html
<section id="section-name">
    <div class="container">
        <div class="section-header">
            <h2>Section Title</h2>
            <p>Supporting description text.</p>
        </div>
        <div class="services-grid">
            <!-- 3 service cards -->
        </div>
    </div>
</section>
```

### Pattern 2: Stats row (dark section)

```html
<section class="stats-section">
    <div class="container">
        <div class="stats-grid">
            <div class="stat-item">
                <h2>500+</h2>
                <p>Brands Transformed</p>
            </div>
            <!-- 4 stat items -->
        </div>
    </div>
</section>
```

### Pattern 3: Card with icon badge

```html
<div class="service-card">
    <div class="icon-badge">
        <!-- SVG icon, 40x40, stroke #121317, stroke-width: 2 -->
    </div>
    <h3>Title</h3>
    <p>Description text.</p>
</div>
```

### Pattern 4: Testimonial card

```html
<div class="testimonial-card">
    <div class="stars">★★★★★</div>
    <blockquote>"Quote text here."</blockquote>
    <div class="testimonial-author">
        <div class="testimonial-avatar">SK</div>
        <div class="testimonial-info">
            <h4>Name</h4>
            <p>Title, Company</p>
        </div>
    </div>
</div>
```

### Pattern 5: CTA section (dark)

```html
<section id="contact" class="cta-section">
    <div class="container">
        <h2>Ready to Elevate Your Brand?</h2>
        <p>Supporting copy that drives action.</p>
        <div class="cta-buttons">
            <a href="#" class="btn btn-primary-inverse">Primary CTA</a>
            <a href="#" class="btn btn-secondary-inverse">Secondary CTA</a>
        </div>
    </div>
</section>
```

---

## 12. Quick Start Template

Minimal starting point for any new page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Title</title>
    <link href="https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;450;500&display=swap" rel="stylesheet">
    <style>
        /* === Design System Variables === */
        :root {
            --ag-black: #121317;
            --ag-white: #ffffff;
            --ag-gray-muted: #45474d;
            --ag-gray-light: rgba(183, 191, 217, 0.1);
            --ag-gray-border: rgba(33, 34, 38, 0.06);
            --card-bg: rgba(183, 191, 217, 0.05);
            --icon-badge-bg: rgba(183, 191, 217, 0.09);
        }

        /* === Reset === */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }

        /* === Base === */
        body {
            font-family: "Google Sans Flex", "Google Sans", sans-serif;
            color: var(--ag-black);
            background: var(--ag-white);
            font-size: 16px;
            line-height: 24px;
            -webkit-font-smoothing: antialiased;
        }

        /* === Layout === */
        .container {
            max-width: 1744px;
            margin: 0 auto;
            padding: 0 72px;
        }

        section { padding: 120px 0; }

        /* === Buttons === */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            padding: 10px 24px;
            border-radius: 9999px;
            font-size: 17.5px;
            font-weight: 450;
            letter-spacing: 0.18px;
            line-height: 25.38px;
            text-decoration: none;
            border: none;
            cursor: pointer;
            transition: all 0.15s ease-out;
        }

        .btn-primary {
            background: var(--ag-black);
            color: var(--ag-white);
        }
        .btn-primary:hover { opacity: 0.85; }

        .btn-secondary {
            background: var(--ag-gray-light);
            color: var(--ag-black);
            border: 0.8px solid var(--ag-gray-border);
        }
        .btn-secondary:hover { opacity: 0.85; }

        .btn-primary-inverse {
            background: var(--ag-white);
            color: var(--ag-black);
        }

        .btn-secondary-inverse {
            background: rgba(183, 191, 217, 0.2);
            color: var(--ag-white);
            border: 0.8px solid rgba(230, 234, 240, 0.06);
        }

        /* === Cards === */
        .card {
            background: var(--card-bg);
            border: 0.8px solid var(--ag-gray-border);
            border-radius: 24px;
            padding: 32px;
            transition: transform 0.15s ease-out;
        }
        .card:hover { transform: translateY(-4px); }

        /* === Section Header === */
        .section-header {
            text-align: center;
            margin-bottom: 64px;
        }
        .section-header h2 {
            font-size: 54px;
            font-weight: 450;
            line-height: 56px;
            letter-spacing: -0.95px;
            margin-bottom: 16px;
        }
        .section-header p {
            color: var(--ag-gray-muted);
            max-width: 600px;
            margin: 0 auto;
        }

        /* === Responsive === */
        @media (max-width: 1200px) {
            .container { padding: 0 40px; }
        }
        @media (max-width: 768px) {
            .container { padding: 0 24px; }
            section { padding: 80px 0; }
            .section-header h2 { font-size: 36px; line-height: 44px; }
        }
    </style>
</head>
<body>
    <!-- Your content here -->
</body>
</html>
```

---

## 13. Apply Checklist

Use this checklist when applying the design system to a new website:

### Foundation
- [ ] Copy CSS variables block into `:root`
- [ ] Add Google Sans font link in `<head>`
- [ ] Set `font-family: "Google Sans Flex", "Google Sans", sans-serif` on `body`
- [ ] Set `scroll-behavior: smooth` on `html`
- [ ] Set up `.container` with `max-width: 1744px` and `padding: 0 72px`

### Components
- [ ] Create `.btn`, `.btn-primary`, `.btn-secondary`, `.btn-primary-inverse`, `.btn-secondary-inverse` classes
- [ ] Set up `.card` with `transparent-bg + border + 24px radius`
- [ ] Build `.section-header` with h2 at `54px`, `letter-spacing: -0.95px`
- [ ] Add `.icon-badge` class: 98px circle, `icon-badge-bg` fill, 40px SVG inside

### Header & Navigation
- [ ] Add fixed header with 52px height, blur backdrop, 0.8px border-bottom
- [ ] Wire up scroll-hide JavaScript (hide on scroll-down, show on scroll-up)
- [ ] Style nav links at 14.5px, weight 450, hover opacity 0.7

### Grids
- [ ] 3-column grid for services, testimonials, blog (class: `.services-grid`)
- [ ] 2-column grid for features (class: `.features-grid`)
- [ ] 4-column grid for stats (class: `.stats-grid`)
- [ ] 4-column footer grid with 2fr for brand column

### Dark Sections
- [ ] Switch `--ag-black` ↔ `--ag-white` backgrounds
- [ ] Use inverse button variants in dark sections
- [ ] Set muted text at `rgba(255, 255, 255, 0.7)`

### Interactive States
- [ ] All buttons: `opacity: 0.85` on hover (0.9 for inverse variants)
- [ ] All cards: `transform: translateY(-4px)` on hover
- [ ] All links: `opacity` or `color` transition at `0.15s ease-out`

### Typography
- [ ] Headings: `font-weight: 450`
- [ ] Section headings: `letter-spacing: -0.95px`
- [ ] Body: `line-height: 24px`, `-webkit-font-smoothing: antialiased`

### Responsive
- [ ] All grids → single column on mobile
- [ ] Typography scales down on mobile (h1: 80px→48px, h2: 54px→36px)
- [ ] Container padding: 72px → 40px → 24px
- [ ] Section padding: 120px → 80px on mobile
- [ ] Footer grid: 4 columns → 2 columns on mobile
- [ ] Nav hidden on mobile (hamburger menu)

---

## Design System at a Glance

```
ONE ACCENT COLOR
└── #121317 (ag-black)
    → buttons, text, icons, borders

ONE FONT
└── Google Sans (400/450/500)
    → everything, no exceptions

THREE CARD VARIANTS
└── Service card (icon-badge top)
└── Feature card (image + button)
└── Testimonial card (stars + avatar)

FOUR BUTTON VARIANTS
└── Primary (black) / Primary Inverse (white)
└── Secondary (light) / Secondary Inverse (dark)

FOUR SECTION TYPES
└── Light + grid (services, features, testimonials, blog)
└── Dark + grid (stats)
└── Dark + centered (CTA)
└── Dark + footer columns (footer)

TWO GRID SYSTEMS
└── 3-column: gap 24px, card padding 32px, radius 24px
└── 2-column: same spacing, for features

ONE BORDER VALUE
└── 0.8px solid rgba(33, 34, 38, 0.06)

ZERO SHADOWS
└── Depth via transparent backgrounds + hover lift (-4px)
```

---

*Built from the Gravitonic Digital Marketing Agency landing page. Any new site that starts with this CSS block and follows the patterns above will match this design language exactly.*