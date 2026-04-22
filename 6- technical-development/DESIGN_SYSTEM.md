# Indikin Design System Reference

> **For AI Agents:** This file is a machine-readable reference for every reusable CSS class, design token, and component pattern in the Indikin front-end. Use it to write code that exactly matches the existing design.

---

## 1. CSS Custom Properties (Design Tokens)

Defined in `src/index.css` under `@layer base { :root { … } }`.

```css
:root {
  /* ── Brand Colors ── */
  --primary:          #FF1493;       /* Deep Pink */
  --primary-rgb:      255, 20, 147;  /* For rgba() usage */
  --primary-light:    #ff85c2;       /* Hover / light accent */
  --primary-dark:     #d10072;       /* Active / pressed */
  --gradient-start:   #FF1493;       /* = primary */
  --gradient-end:     #8A2BE2;       /* = purple */
  --purple:           #8A2BE2;       /* Blue Violet */
  --purple-rgb:       138, 43, 226;

  /* ── Surfaces ── */
  --background:       #0A0A0A;       /* Page bg */
  --card:             #141414;       /* Card / modal bg */
  --card-rgb:         20, 20, 20;
  --card-border:      #222222;
  --muted:            #282828;       /* Muted surfaces */
  --border-muted:     #2a2a2a;       /* Subtle borders */

  /* ── Text ── */
  --text:             #ffffff;
  --text-secondary:   #a3a3a3;
  --muted-foreground: #a3a3a3;       /* = text-secondary */
}
```

### Additional Hard-Coded Surface Colors

| Hex | Tailwind Class | Usage |
|-----|----------------|-------|
| `#0e0e0e` | `bg-[#0e0e0e]` | `.section-dark` |
| `#0d0d0d` | — | `.hero-v2` |
| `#1a1a1a` | `bg-[#1a1a1a]` | Form inputs |
| `#1f1f1f` | `bg-[#1f1f1f]` | Payment modal header, datepicker bg, tooltip bg |
| `#2a2a2a` | `bg-[#2a2a2a]` | Search bg, datepicker header, social buttons bg |
| `#151515` | — | `.bg-card-dark` |
| `#555` | — | Pagination dots (inactive) |

---

## 2. Tailwind Color Aliases

Defined in `tailwind.config.js` → `theme.extend.colors`:

```js
colors: {
  primary:           'var(--primary)',
  'primary-light':   'var(--primary-light)',
  'primary-dark':    'var(--primary-dark)',
  'primary-hover-bg':'rgba(var(--primary-rgb), 0.1)',
  'primary-10':      'rgba(var(--primary-rgb), 0.1)',
  background:        'var(--background)',
  card:              'var(--card)',
  muted:             'var(--muted)',
  'muted-foreground':'var(--muted-foreground)',
  'border-muted':    'var(--border-muted)',
  text:              'var(--text)',
  'text-secondary':  'var(--text-secondary)',
  purple:            'var(--purple)',
  'gradient-start':  'var(--gradient-start)',
  'gradient-end':    'var(--gradient-end)',
  'search-bg':       '#2a2a2a',
  'search-border':   '#3a3a3a',
}
```

### Additional Tailwind Customizations

```js
maxWidth: {
  'lg-plus': '36rem',   // 576px — used for constrained content areas
},
transitionProperty: {
  'height': 'height',
  'spacing': 'margin, padding',
  'width': 'width',
  'margin': 'margin',
},
```

### Tailwind Plugins

- **`@tailwindcss/typography`** — provides `.prose` classes for rendered Markdown content (e.g., Litepaper modal, legal pages).

---

## 3. Typography Classes

### Font Families (Tailwind Config)

```js
fontFamily: {
  sans: ['Inter', ...defaultTheme.fontFamily.sans],  // Default body
  montserrat: ['Montserrat', 'sans-serif'],          // Headlines
}
```

### Heading Selectors (CSS)

All `h1`–`h6` tags and their scoped variants (`section h1`, `article h2`, `nav h3`, `aside h4`, etc.) are globally styled **outside `@layer`** (lines 210–288 in `index.css`), giving them higher specificity than Tailwind base resets:

```css
/* Outside @layer — high specificity */
h1, h2, h3, h4, h5, h6,
section h1, article h1, nav h1, aside h1, /* etc. */ {
  @apply font-bold text-white;
  font-family: 'Montserrat', sans-serif;
}
```

| Tag | Mobile Size | Desktop Size (≥md) | Margin-Bottom |
|-----|-------------|---------------------|---------------|
| `h1` | `text-4xl` | `text-5xl` | `mb-6` |
| `h2` | `text-3xl` | `text-4xl` | `mb-5` |
| `h3` | `text-2xl` | `text-3xl` | `mb-4` |
| `h4` | `text-xl` | `text-2xl` | `mb-4` |
| `h5` | `text-lg` | `text-xl` | `mb-3` |
| `h6` | `text-base` | `text-lg` | `mb-3` |

### Notable Text Classes

| Class | Effect |
|-------|--------|
| `.pink` | `color: var(--primary)` |
| `.gradient-text` | `background: linear-gradient(to right, var(--gradient-start), var(--gradient-end)); -webkit-background-clip: text; -webkit-text-fill-color: transparent;` |
| `.font-montserrat` | `font-family: 'Montserrat', 'sans-serif'` |
| `.visually-hidden` | Screen-reader-only (abs positioned, 1px clip) |

---

## 4. Button System

### Base Class

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 0.5rem;      /* rounded-lg */
  padding: 0.75rem 1.5rem;    /* py-3 px-6 */
  font-weight: 600;           /* font-semibold */
  font-size: 0.95rem;
  letter-spacing: 0.05em;     /* tracking-wider */
  height: 42px;
  transition: all 200ms;
  cursor: pointer;
}
```

### Variants Reference

| Class | Background | Border | Text | Hover Effect | Shadow |
|-------|-----------|--------|------|-------------|--------|
| `.btn-primary` | `var(--primary)` | none | white | Gradient bg; lift -1px; stronger shadow | `0 4px 12px rgba(primary, 0.2)` |
| `.btn-outline` | transparent | `1px solid var(--muted)` | `var(--text-secondary)` | Gradient bg 10%; pink border; lift | none → `0 4px 12px rgba(0,0,0,0.15)` |
| `.btn-outline-primary` | transparent | `1px solid var(--primary)` | white | `primary-hover-bg`; lighter border | — |
| `.btn-danger` | `red-600` | none | white | `red-700`; lift | `0 4px 12px rgba(220,38,38,0.2)` |
| `.btn-danger-outline` | transparent | `red-500/50` | `red-400` | `red-500/10` bg; `red-300` text; lift | — |
| `.btn-golden` | Gold gradient | none | black | Gold glow shadow | — |
| `.btn-connect-wallet` | `var(--primary)` | none | white | Gradient; lift | `0 4px 12px rgba(primary,0.2)` |
| `.btn-animate-scroll` | transparent | `var(--primary)` | white | When `.scrolled`: fill pink bg → gradient on hover | — |

### Disabled States

```css
:disabled {
  background: var(--muted);
  color: var(--muted-foreground);
  cursor: not-allowed;
  box-shadow: none;
  transform: none;
  opacity: 0.7;
}
```

---

## 5. Card System

### Base Card

```css
.card {
  background: var(--card);
  border: 1px solid var(--muted);
  border-radius: 0.5rem;
  overflow: hidden;
  transition: all 300ms ease-in-out;
  position: relative;
}
.card:hover {
  transform: translateY(-5px);
  border-color: rgba(var(--primary-rgb), 0.3);
}
```

### Pass Card

```css
.pass-card {
  background: var(--card);
  border: 1px solid var(--muted);
  border-radius: 1rem;          /* rounded-2xl */
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
  /* Active slide gets purple glow via ::after */
}
```

### Film Card

```css
.film-card {
  border-radius: 0.5rem;
  overflow: hidden;
  background: var(--card);
}
.film-card:hover .film-thumbnail {
  transform: scale(1.05);
}
```

### Filmmaker Card

Composite card with cover image (180px), avatar overlay (-12 offset), stats footer with token price, and social icons row.

---

## 6. Form System

```css
.form-label   → text-sm font-medium text-text-secondary text-left mb-2
.form-input   → bg-[#1a1a1a] border-[#2a2a2a] rounded-lg py-3 px-4 text-white
.form-input:focus → border: var(--primary), outline none
.form-select-arrowed → custom SVG arrow, padding-right 2.5rem
```

### Autofill Override

```css
input:-webkit-autofill {
  -webkit-text-fill-color: #ffffff;
  -webkit-box-shadow: 0 0 0px 1000px #141414 inset;
  caret-color: #fff;
}
```

---

## 7. Modal System

| Property | Value |
|----------|-------|
| Background | `var(--card)` |
| Border radius | `rounded-xl` (0.75rem) |
| Max height | `90vh` |
| Overflow | `overflow-y-auto` |
| Shadow | `0 25px 50px -12px rgba(0,0,0,0.4)` |
| Border | `1px solid rgba(60,60,60,0.5)` |
| Entry animation | Scale 0.95→1 + translateY(20px→0), 300ms |
| Body padding | `p-6 md:p-8` |

---

## 8. Layout Patterns

### Header / Navigation

```css
.header-container {
  background-color: rgba(17, 17, 17, 0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 10px 15px rgba(0,0,0,0.1);
}
```

### Hero Section

```css
.hero {
  min-height: 560px;
  padding: 3rem 0;  /* py-12, md:py-20 */
  background-size: cover;
  background-position: center top;
  /* ::before = dark gradient overlay */
  /* ::after = subtle noise texture */
}
```

### Content Sections

```css
.section        → py-16 md:py-20 relative
.section-dark   → bg-[#0e0e0e]
.section h2     → mb-10 tracking-wide
.section p      → text-text-secondary leading-relaxed mb-6
```

### Footer

```css
.footer {
  background: var(--background);
  border-top: 1px solid var(--muted);
  padding: 3rem 1.5rem;  /* py-12 md:py-16 px-6 md:px-8 */
}
/* Grid: 1col → sm:2col → lg: brand(minmax 250px) + 3×link(minmax 150px) */
```

### Performance: Content Visibility

```css
#indikin-pass, #featured-films, #founding-filmmakers {
  content-visibility: auto;
  contain-intrinsic-size: 1px 800px; /* or 600px for smaller sections */
}
```

---

## 9. Swiper / Carousel System

### Filmmaker Swiper

| Property | Final Value | Source (Line) |
|----------|-------------|---------------|
| Slide width | `340px` (max 90vw) | `.filmmaker-swiper .swiper-slide` (initial def) |
| Inactive scale | `0.9` | `transform: scale(0.9)` (initial def) |
| Active scale | `1.0` | `.swiper-slide-active { transform: scale(1.0) }` (initial def) |
| Contain | `content` | `contain: content` on `.filmmaker-swiper` (~L1845) |
| Min-height | `520px` | `.filmmaker-swiper { min-height: 520px }` (L1848) |

### Film Swiper

> ⚠️ **CSS Override Warning:** Film swiper has **two definition blocks** in `index.css`. The first block (~L1140–1196) defines initial styles; the second "OPTIMIZATION" block (~L1814–1880) **overrides** width, scale, and opacity. The values below reflect the **final computed values**.

| Property | Final Value | Defined At | Overridden At |
|----------|-------------|------------|---------------|
| Slide width | **`380px`** (max 90vw) | `320px` (L1150) | `380px` (L1828) |
| Inactive scale | `0.9` | `scale(0.9)` (L1151) | `scale(0.9)` (L1873) |
| Inactive opacity | **`0.5`** | *(not set)* | `opacity: 0.5` (L1872) |
| Active scale | **`1.0`** | `scale(1.05)` (L1156) | `scale(1)` (L1879) |
| Active opacity | `1.0` | *(not set)* | `opacity: 1` (L1878) |
| Active z-index | `10` | `z-10` (L1155) | `z-index: 10` (L1867) |
| Contain | `content` | `contain: content` (L1142) | also (L1817) |
| Min-height | `380px` | *(not set)* | `min-height: 380px` (L1819) |

### Tier/Pass Swiper

> ⚠️ **CSS Override Warning:** Same dual-block pattern. First block (~L800–856) and second "OPTIMIZATION" block (~L1836–1880).

| Property | Final Value | Defined At | Overridden At |
|----------|-------------|------------|---------------|
| Slide width | `360px` (max 90vw) | `w-[360px] max-w-[90vw]` (L805) | `360px; max-width: 90vw` (L1857) |
| Inactive scale | `0.85` | `scale(0.85)` (L807) | `scale(0.9)` (L1873) ⚠️ |
| Inactive opacity | `0.5` | `opacity-50` (L805) | `opacity: 0.5` (L1872) |
| Active scale | `1.0` | `scale(1)` (L820) | `scale(1)` (L1879) |
| Active opacity | `1.0` | `opacity-100` (L819) | `opacity: 1` (L1878) |
| Active effect | Purple border glow | `.pass-card::after` (L833–856) | *(not overridden)* |
| Contain | `content` | *(not set)* | `contain: content` (L1838) |
| Min-height | `540px` | *(not set)* | `min-height: 540px` (L1840) |

> ⚠️ **Tier swiper inactive scale conflict:** The first block sets `scale(0.85)` (L807) but the shared optimization block sets `scale(0.9)` (L1873) for `:not(.swiper-slide-active)`. The later rule wins, making the **effective inactive scale `0.9`**, not `0.85`. However, the first block also has `will-change: transform` selectors (L813-815) that promote active/adjacent slides. The visual difference may be subtle but the CSS cascade makes `0.9` the winner.

### Pagination

```css
.pagination-dot          → 9px circle, bg #555, opacity 0.6
.pagination-dot.adjacent → scale(1.25), opacity 0.8
.pagination-dot.active   → bg primary, scale(1.75), opacity 1, pink glow shadow
```

---

## 10. Special UI Patterns

### Gradient Border (Animated)

Used on `.gradient-border` elements. The `::after` pseudo-element creates an animated gradient border using CSS mask compositing.

> ⚠️ **CSS Override Warning:** This class is defined **twice** in `index.css`. The first definition (L581–595) uses `p-px` (1px padding) and `rounded-3xl`. The second definition (L1283–1296) uses `padding: 3px` and `border-radius: 24px`. Both are in `@layer components`. The **second definition wins** — the actual border width is **3px**.

```css
/* First definition (L581-595) — OVERRIDDEN */
.gradient-border {
  @apply relative rounded-3xl overflow-hidden bg-card;
}
.gradient-border::after {
  @apply absolute inset-0 rounded-3xl p-px z-0;  /* ← p-px = 1px */
  /* ...mask + animation... */
}

/* Second definition (L1283-1296) — THIS WINS */
.gradient-border::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 24px;     /* 1.5rem, slightly different from rounded-3xl */
  padding: 3px;            /* ← 3px — OVERRIDES the earlier p-px */
  background: linear-gradient(to right, var(--primary), var(--purple), var(--primary));
  background-size: 200% auto;
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
  animation: borderRotate 4s linear infinite;
}
```

**Effective values:** `padding: 3px`, `border-radius: 24px`, `background-size: 200% auto`, `animation: borderRotate 4s linear infinite`.

### Shine Effect (Hover)

```css
.shine-effect::before {
  background: linear-gradient(110deg, transparent 20%,
    rgba(255,255,255,0.07) 45%, rgba(255,255,255,0.07) 55%, transparent 80%);
  transform: translateX(-100%);  /* hover → translateX(100%) */
}
```

### Typing Animation

```css
.animate-typing {
  border-right: .15em solid var(--primary);
  animation: typing-width 5.5s steps(5) infinite,
             fading 5.5s linear infinite,
             blink-caret .75s step-end infinite;
}
```

### Cookie Banner

```css
.cookie-banner {
  background: rgba(var(--card-rgb), 0.9);
  backdrop-filter: blur(8px);
  z-index: 999;
  transform: translateY(100%);  /* .show → translateY(0) */
}
```

### Sold-Out State

```css
.pass-card.sold-out {
  opacity: 0.6;
  filter: grayscale(1);
  border-color: neutral-800;
}
.sold-out-badge {
  background: red-600;
  transform: translate(-50%, -50%) rotate(-12deg);
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}
```

### Live Indicator

```css
.live-dot {
  width: 10px; height: 10px;
  background-color: #39D391;
  box-shadow: 0 0 8px 2px rgba(57, 211, 145, 0.7);
  animation: pulse-glow 2s infinite ease-in-out;
}
```

---

## 11. Custom & Complex Components

### 11.1 Datepicker Theme (`.indikin-datepicker-theme`)
Overrides `react-datepicker` default styles entirely to match dark mode:
- Background: `#1f1f1f` for body, `#2a2a2a` for header
- Selected items: `bg-primary`, Keyboard-selected: `bg-primary-dark`
- Hidden triangles: `.react-datepicker__triangle { display: none !important; }`

### 11.2 Tooltips (`.tooltip`)
Pure CSS tooltip triggered gracefully via parent wrapper (`.coming-soon-wrapper`):
- Start state: `invisible opacity-0`
- Target state: `visible opacity-100` on `:hover, :focus, :focus-within, :active`
- Arrow generated via CSS borders on `::after` element.

### 11.3 Device-Aware Hovers & Overlays
Used for `.film-card-desc-overlay` and `.film-card-info-btn`:
- **Desktop Only:** Enwrapped in `@media (hover: hover) and (pointer: fine)` to ensure overlays slide up (translateY) only on mouse interaction.
- **Touch Devices:** Overlays are fully hidden (`display: none`) or permanently shown, depending on the UX pattern.

### 11.4 Time Progression Bar (`.time-indicator-progress`)
Simulates video playback progress without JavaScript repaints on width:
- Core technique: Uses `transform: translateX(...)` with a `max()` clamp to ensure the minimum label width (95px) always remains visible even at 0%.

### 11.5 Custom Webkit Scrollbars (`.desc-modal-scrollbar`)
Narrow elegant scrollbars for modals:
- Width: `4px`
- Thumb: `rgba(255, 255, 255, 0.2)` rounding via `border-radius: 9999px`.

### 11.6 Payment UI Controls
- **Segmented Control:** `.payment-segmented-control`. A toggle bar container mimicking iOS segmented controls, switching button `bg-[#2a2a2a]` → `bg-primary` on active via local transitions.
- **Card Flip (`.redeem-card-flipper`)**: 3D card flip animation `rotateY(180deg)` with `transform-style: preserve-3d` and `backface-visibility: hidden` for redemption mechanics.
- **Status View**: Success (`text-green-400` / light green bg bubble) and Error (`text-red-400` / light red bg bubble) for visual post-payment feedback.

### 11.7 Video Player UI (`.video-overlay-container`)
Smart overlay hiding logic using `.idle`:
- Transition: `opacity-100` to `.idle { opacity-0 }`
- `.video-overlay-button`: Glassmorphic control buttons (`bg-black/30 backdrop-blur-sm`).
