# Indikin Brand Identity

> **© 2025 Indikin.online. All Rights Reserved. Made with ❤️ by YalaCoder.**

---

## 1. Mission & Vision

**Mission:** Accelerate the way indie filmmakers are financed and their productions distributed, providing a decentralised and inclusive platform for investors, filmmakers, and their audiences.

**Vision:** A unified decentralised filmmaker ecosystem that bridges Web3 infrastructure with Web2 creators, enabling token-based revenue sharing, community-powered funding, and global distribution through a native streaming platform.

**Tagline:** *Decentralized Filmmaker Ecosystem*

---

## 2. Brand Hierarchy

| Entity | Role | URL |
|--------|------|-----|
| **Indikin** | Umbrella brand for the entire ecosystem | `indikin.com` |
| **Indikin.online** | Production platform (IndiFlix streaming, dashboard, creator tools) | `indikin.online` |
| **IndiFlix** | Sub-brand for the streaming/content experience within Indikin.online | N/A — section within `indikin.online/dashboard` |
| **$INDIKIN** | Native PRC-20 token on PulseChain | Contract: `0xC0372486fCab952aA2B7998876d6aa79d4Fc1938` |
| **Indikin Production Fund** | Gnosis Safe multisig treasury | `0x44D8Ca8Ec21399e138b64981E6BF0caCfB746D26` |
| **Indikin Token Index** | Index of all filmmaker tokens bonded to $INDIKIN | N/A — on-chain concept |
| **Indikin Pass** | Subscription product (yearly tiers + Angel Pass lifetime) | Purchase flow within `indikin.online` |

### Pass Tiers (Backend-Enforced Pricing)

| Tier ID | Price | Name | Status |
|---------|-------|------|--------|
| `stage1` | — | Stage 1 Indikin Pass | **SOLD OUT** (removed from backend) |
| `stage2` | $99.00/yr ($8.25/mo) | Stage 2 Indikin Pass | Current |
| `stage3` | $149.00/yr | Stage 3 Indikin Pass | Future |
| `stage4` | $199.00/yr | Stage 4 Indikin Pass | Future |
| `stage5` | $249.00/yr | Stage 5 Indikin Pass | Future |
| `lifetime` | $999.00 | Angel Pass (3+ years) | Limited availability |

---

## 3. Logo & Favicon Assets

All logos reside in `public/assets/img/`:

| Asset | Path | Format | Purpose |
|-------|------|--------|---------|
| Primary Logo (small) | `logo.png` / `logo.webp` | PNG / WebP | Footer logo (40×40 rounded), emails |
| Primary Logo (large) | `indikin-logo.png` | PNG | Navbar (h-10), OG cards |
| Primary Logo (XL) | `indikin-logo-1.png` | PNG | Print, presentations (72KB) |
| Vector Logo | `indikin-logo.svg` | SVG | Scalable use cases (28KB) |
| Favicon (WebP) | `favicon.webp` | WebP | Primary favicon (modern browsers) |
| Favicon (PNG) | `favicon.png` | PNG | Favicon fallback |
| Favicon (ICO) | `favicon.ico` | ICO 32×32 | Legacy browser tab |
| Social Share Card | `social-share-card.png` | PNG 180KB | Open Graph / Twitter cards |
| Social Share Card v2 | `social-share-card2.png` | PNG 248KB | Alternative share card |
| Indi AI Avatar | `Indi_AI.png` | PNG 44KB | AI assistant avatar |
| Apple Touch Icon | `logo.png` | PNG | iOS home screen |
| PulseChain Logo | `pls-logo.png` | PNG 33KB | Token ecosystem display |
| Brian Portrait | `brian.jpg` | JPG 102KB | Filmmaker card |
| Bitjoin Studios | `bitjoin-studios.png` | PNG 80KB | Filmmaker card |
| IndiFlx Hero | `indiflix_hero.jpg` | JPG 382KB | Alternative hero image |
| Dextop | `dextop.png` | PNG 74KB | Ecosystem display |
| `avatars/` | Directory | — | Filmmaker avatar images |
| `covers/` | Directory | — | Filmmaker cover images |
| Hero BG Desktop Alt | `hero-bg-desktop1.webp` | WebP 87KB | Alternative desktop hero |

**Logo usage rules:**
- Navbar uses `indikin-logo.png` at `h-10` (40px) with `w-auto`.
- Footer uses `logo.png`/`logo.webp` at 40×40, rounded-full, inside a `<picture>` element with WebP source.
- The logo text reads: `INDIKIN` (white) + `.online` (primary pink).
- Always use the WebP variant for web contexts; PNG for emails.
- SVG is the canonical scalable format for any print or high-DPI use.

---

## 4. Color Palette

### 4.1 Primary Colors (CSS Custom Properties)

Defined in `:root` within `src/index.css` and `index.html`:

| Token | Hex | RGB | Usage |
|-------|-----|-----|-------|
| `--primary` | `#FF1493` | `255, 20, 147` | **Deep Pink** — primary brand color, CTA buttons, active states, links, accents |
| `--primary-light` | `#ff85c2` | — | Hover state of primary, lighter accent |
| `--primary-dark` | `#d10072` | — | Active/pressed state, keyboard-focused datepicker |
| `--purple` | `#8A2BE2` | `138, 43, 226` | **Blue Violet** — gradient endpoint, pass card glow, lifetime accent |
| `--gradient-start` | `#FF1493` | — | Gradient left (same as primary) |
| `--gradient-end` | `#8A2BE2` | — | Gradient right (same as purple) |

### 4.2 Background & Surface Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `--background` | `#0A0A0A` | Page background — near-black |
| `--card` | `#141414` | Card surfaces, modals, panels |
| `--card-border` | `#222222` | Card border default |
| `--muted` | `#282828` | Muted background (disabled buttons, dividers) |
| `--border-muted` | `#2a2a2a` | Subtle borders, section dividers |
| `#0e0e0e` | — | `section-dark` variant background |
| `#0d0d0d` | — | `hero-v2` background |
| `#1a1a1a` | — | Form input backgrounds |
| `#1f1f1f` | — | Payment modal header, datepicker background |
| `#2a2a2a` | — | Search background, datepicker header |
| `#151515` | — | `bg-card-dark` variant |

### 4.3 Text Colors

| Token | Hex | Usage |
|-------|-----|-------|
| `--text` | `#ffffff` | Primary text — pure white |
| `--text-secondary` | `#a3a3a3` | Secondary text, labels, descriptions |
| `--muted-foreground` | `#a3a3a3` | Disabled/muted text (same as text-secondary) |

### 4.4 Semantic / Feedback Colors

| Color | Hex / Class | Usage |
|-------|-------------|-------|
| Green | `text-green-500` / `#39D391` | Price up, success states, live indicator |
| Red | `text-red-500` / `red-600` | Price down, danger buttons, error states, sold-out badge |
| Yellow/Gold | `yellow-300` → `yellow-500` gradient | Golden "Angel Pass" button, lifetime highlights |
| Pink variants | `pink-400` | Active payment tab |

### 4.5 Brand Gradient

```css
background: linear-gradient(to right, #FF1493, #8A2BE2);
```

Used for:
- Gradient text (`.gradient-text`)
- Button hover states (`.btn-primary:hover`, `.btn-outline:hover`)
- Animated rotating borders (`.gradient-border`)
- Pass card lifetime borders
- Hero CTA hover

The animated gradient border uses `background-size: 200% auto` with `borderRotate` keyframe animation (4s linear infinite).

### 4.6 Theme Color (Mobile Browser Chrome)

```html
<meta name="theme-color" content="#aa00ff" />
```

---

## 5. Typography

### 5.1 Font Families

| Font | Weights | Role | Source |
|------|---------|------|--------|
| **Inter** | 400, 500, 600, 700 | Body text, UI elements, forms, labels | Google Fonts CDN (`display=optional`) |
| **Montserrat** | 700, 800 | Headlines (h1–h6), prices, pass names, logo text | Google Fonts CDN (`display=optional`) |

**Loading strategy:** Fonts are loaded from the Google Fonts CDN via a `<link>` tag in `index.html`, not from `@fontsource` packages. The `display=optional` strategy prevents FOIT — if fonts haven't loaded by first paint, system fonts are used and the web font won't swap in mid-session. A `<noscript>` fallback link is also provided.

```html
<!-- From index.html -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Montserrat:wght@700;800&display=optional" rel="stylesheet" />
```

### 5.2 Tailwind Font Stack

```js
fontFamily: {
  sans: ['Inter', ...defaultTheme.fontFamily.sans],
  montserrat: ['Montserrat', 'sans-serif'],
}
```

### 5.3 Heading Hierarchy

All headings use `font-family: 'Montserrat', sans-serif` and `font-weight: bold` with white color.

> **Note:** Heading styles are defined **outside** `@layer base` in `index.css` (lines 210–288), targeting `h1–h6` and their scoped variants (`section h1`, `article h2`, `nav h3`, `aside h4`, etc.). This gives them higher specificity than Tailwind base styles.

| Level | Mobile | Desktop (≥768px) | Bottom Margin |
|-------|--------|-------------------|---------------|
| `h1` | `text-4xl` (2.25rem) | `text-5xl` (3rem) | `mb-6` |
| `h2` | `text-3xl` (1.875rem) | `text-4xl` (2.25rem) | `mb-5` |
| `h3` | `text-2xl` (1.5rem) | `text-3xl` (1.875rem) | `mb-4` |
| `h4` | `text-xl` (1.25rem) | `text-2xl` (1.5rem) | `mb-4` |
| `h5` | `text-lg` (1.125rem) | `text-xl` (1.25rem) | `mb-3` |
| `h6` | `text-base` (1rem) | `text-lg` (1.125rem) | `mb-3` |

### 5.4 Body Text

- Line height: `1.6`
- Letter spacing: `0.015em`
- Font smoothing: `-webkit-font-smoothing: antialiased`

---

## 6. Iconography

- **Library:** React Icons (`react-icons` v5.2.1)
- **Style:** Outline-style icons as the default; filled for active/selected states.
- **Size:** Icons in social buttons use `text-lg` (1.125rem); sidebar icons vary.
- **Social platform icons:** Full-color PNG/WebP images in `public/assets/img/` (Telegram, Discord, X/Twitter, YouTube, Reddit, LinkedIn, Facebook, TikTok, Instagram).

---

## 7. Imagery & Media

### 7.1 Hero Backgrounds

Responsive art-directed hero images loaded via `<link rel="preload">` with `imagesrcset` in `index.html`:

| Breakpoint | Asset | Size | Delivery |
|------------|-------|------|----------|
| Mobile (default) | `hero-bg-mobile.webp` | 30KB, 767w | CSS `background-image` in app-shell |
| Tablet (≥768px) | `hero-bg-tablet.webp` | 127KB, 1439w | CSS media query swap |
| Desktop (≥1440px) | `hero-bg-desktop.webp` | 216KB, 1920w | CSS media query swap |
| Desktop Alt | `hero-bg-desktop1.webp` | 87KB | Alternative desktop artwork |

**App Shell Skeleton:** `index.html` renders an `#app-shell-hero` div with a matching hero background, header skeleton (logo placeholder, search bar, button placeholders), and content placeholders. This eliminates CLS (Cumulative Layout Shift) during React hydration. The skeleton auto-hides on non-`/` routes via an inline `<script>`.

Hero overlay: `linear-gradient(to top, rgba(17,17,17,1) 0%, rgba(17,17,17,0.8) 20%, rgba(0,0,0,0.4) 100%)` (`.hero::before`) plus a subtle noise texture via inline SVG data URI (`.hero::after` at `opacity: 0.4`).

### 7.2 Video

- **Platform:** Cloudflare Stream (signed URLs, HLS/DASH)
- **Upload:** TUS protocol via `tus-js-client` for resumable uploads
- **Thumbnails:** Proxied through the Worker API (`/thumbnail/:uid`) with caching
- **Player:** Custom `StreamPlayer.jsx` component with Cloudflare Stream embed
- **Security:** All videos require signed URLs (`requireSignedURLs: true`), enforced at creation and verified post-creation with a fail-closed pattern

### 7.3 Image Delivery

- **Platform:** Cloudflare Images for profile pictures and thumbnails
- **Format:** WebP preferred, PNG fallback
- **Lazy loading:** `IntersectionObserver` via custom `LazyLoad.jsx` component

---

## 8. UI Component Styling

### 8.1 Buttons

| Class | Appearance | Hover | Active |
|-------|------------|-------|--------|
| `.btn` | Base: `inline-flex`, `rounded-lg`, `px-6 py-3`, `h-[42px]`, `font-semibold`, `tracking-wider` | — | — |
| `.btn-primary` | Pink bg (`--primary`), white text, subtle pink box-shadow | Gradient bg (pink→purple), lift `-1px` | Press `+1px` |
| `.btn-outline` | Transparent bg, muted border, secondary text | Gradient bg at 10% opacity, pink border, lift | Press |
| `.btn-danger` | Red-600 bg, white text | Darken to red-700, lift | Press |
| `.btn-danger-outline` | Transparent bg, red-500/50 border, red-400 text | Lighten text, lift | Press |
| `.btn-golden` | Gold gradient (`yellow-300` → `yellow-500`), black text | Gold glow `box-shadow` | — |
| `.btn-connect-wallet` | Same as btn-primary with overflow hidden | Gradient + lift | — |
| `.btn-animate-scroll` | Transparent with pink border; transitions to filled on scroll | Gradient on hover | — |

### 8.2 Cards

```css
.card {
  background: var(--card);       /* #141414 */
  border: 1px solid var(--muted); /* #282828 */
  border-radius: 0.5rem;         /* rounded-lg */
  transition: all 300ms;
}
.card:hover {
  transform: translateY(-5px);
  border-color: rgba(255, 20, 147, 0.3); /* primary at 30% */
}
```

### 8.3 Forms

| Element | Style |
|---------|-------|
| `.form-label` | `text-sm`, `font-medium`, secondary text color, left-aligned |
| `.form-input` | `bg-[#1a1a1a]`, `border-[#2a2a2a]`, `rounded-lg`, `py-3 px-4`, white text |
| `.form-input:focus` | Pink border (`--primary`) |
| Autofill | Black bg (`#141414`), white text via `-webkit-box-shadow` inset hack |

### 8.4 Modals

- Container: `.modal-content-base` — `bg-card`, `rounded-xl`, `max-h-[90vh]`, `overflow-y-auto`
- Entry animation: Scale from 0.95 + translateY(20px) → scale(1) + translateY(0) on `.animate-fade-in`
- Shadow: `0 25px 50px -12px rgba(0,0,0,0.4)`
- Border: `1px solid rgba(60,60,60,0.5)`

### 8.5 Navigation

- **Header:** Sticky, `bg rgba(17,17,17,0.85)`, `backdrop-filter: blur(12px)`, bottom border `white/10`
- **Mobile menu:** Slide-in animation, full-height overlay
- **Search bar:** Centered, max-width 672px, pill-shaped (`rounded-full`), `bg rgba(255,255,255,0.1)`

---

## 9. Motion & Animation

### 9.1 Named Animations (Tailwind + CSS Keyframes)

| Animation | Duration | Easing | Purpose |
|-----------|----------|--------|---------|
| `borderRotate` | 4s linear ∞ | Linear | Animated gradient border rotation |
| `fade-in` | 0.5s ease-out | Ease-out | Page/modal fade in |
| `fade-in-fast` | 0.2s ease-out | Ease-out | Quick element reveal |
| `typing` / `typing-hero` | 5.5s / 6s | Steps | Typewriter text effect on hero |
| `blink-caret` | 0.75s step-end ∞ | Step-end | Typing cursor blink |
| `rocket-launch-main` | 0.8s ease-out ∞ | Alternating | Rocket icon float animation |
| `rocket-smoke` | 0.8s ease-out ∞ | Ease-out | Smoke particles below rocket |
| `shake` | 0.82s cubic-bezier | Bounce | Error shake feedback |
| `slide-in-left/right` | 0.3s ease-out | Ease-out | Panel slide transitions |
| `slide-in-down` | 0.3s ease-out | Ease-out | Dropdown reveal |
| `redeem-flip` | 1s ease-out | Ease-out | Pass card 3D flip |
| `redeem-shine` | 3s ease-in-out ∞ | Ease-in-out | Shine sweep on lifetime pass |
| `chart-bar-grow` | 0.5s cubic-bezier | Smooth | Bar chart growth animation |
| `pulse-glow` | 2s ease-in-out ∞ | Ease-in-out | Live indicator dot pulse |
| `shine` | 1.5s ease-in-out | Ease-in-out | Shine sweep on cards |

### 9.2 Micro-Interactions

- **Button hover:** `-translate-y-1px` lift with expanded box-shadow
- **Button active:** `translate-y-1px` press
- **Card hover:** `translateY(-5px)` with pink border glow
- **Swiper slides:** Scale 0.9 → 1.0 (active) with opacity 0.5 → 1.0 transitions
- **Shine effect:** Hover-triggered diagonal light sweep via `::before` pseudo-element
- **Tooltip:** `invisible` → `visible` with opacity fade on hover/focus

---

## 10. Spacing, Layout & Breakpoints

### 10.1 Breakpoints (Tailwind Defaults)

| Prefix | Min-Width |
|--------|-----------|
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |
| `2xl` | 1536px |

### 10.2 Section Spacing

- `.section`: `py-16` (mobile) / `py-20` (≥md)
- `.footer`: `py-12` (mobile) / `py-16` (≥md), `px-6` (mobile) / `px-8` (≥md)
- Container: `max-w-7xl mx-auto`
- `.hero`: `min-h-[560px]`, `py-12` (mobile) / `py-20` (≥md)

### 10.3 Footer Grid

```css
/* Mobile: 1 col | SM: 2 col | LG: 4 col (brand + 3 link groups) */
grid-template-columns: minmax(250px, 1fr) repeat(3, minmax(150px, 1fr));
```

---

## 11. Social Presence

### 11.1 Official Channels

The Footer component (`Footer.jsx`) renders **11 social icons** using React Icons. The Worker API (`worker.js`) provides `/social/*` redirect routes for **9** of these.

| Platform | Icon Component | URL (Footer) | Worker Redirect |
|----------|---------------|-------------|------------------|
| Telegram | `FaTelegram` | `t(common.social.telegramUrl)` *(i18n key)* | `/social/telegram` → `t.me/+uC-rKNh6BFw3MzI8` |
| Discord | `FaDiscord` | `discord.gg/3CnX4F3QkY` | `/social/discord` → same |
| X / Twitter | `FaXTwitter` (from `react-icons/fa6`) | `x.com/IndiKinofficial` | `/social/twitter` → same |
| YouTube | `FaYoutube` | `youtube.com/@IndiKin` | `/social/youtube` → same |
| Reddit | `FaRedditAlien` | `reddit.com/r/indikin` | `/social/reddit` → same |
| LinkedIn | `FaLinkedin` | `linkedin.com/showcase/indikin` | `/social/linkedin` → same |
| Facebook | `FaFacebook` | `facebook.com/indikinofficial` | `/social/facebook` → same |
| TikTok | `FaTiktok` | `tiktok.com/@indikinoffical` ⚠️ | `/social/tiktok` → `tiktok.com/@indikinofficial` |
| Instagram | `FaInstagram` | `instagram.com/indikinoffical` ⚠️ | `/social/instagram` → `instagram.com/indikinofficial` |
| Clubhouse | `SiClubhouse` (from `react-icons/si`) | `clubhouse.com/house/indikinonline` | *(no redirect)* |
| Bluesky | `SiBluesky` (from `react-icons/si`) | `bsky.app/profile/indikin.bsky.social` | *(no redirect)* |

> ⚠️ **Known Discrepancy:** The Footer component has TikTok and Instagram URLs with a typo (`indikinoffical`) while the Worker redirect routes have the correct spelling (`indikinofficial`).

### 11.2 Contact

- **Primary email:** `info@indikin.com`
- **System email (sender / Resend):** `hello@indikin.online`
- **Admin notification recipients:** `info@indikin.com`, `indikinonline@gmail.com`
- **External blog:** `https://bitjoinstudios.com/blog/` (linked in Footer resources)

---

## 12. Tone of Voice

### 12.1 Principles

1. **Empowering:** Speak to filmmakers as fellow creatives. "You own the content; you set the terms."
2. **Community-first:** Use "we" and "our" language. Audiences are part of the team.
3. **Clear & Direct:** Avoid jargon when possible. When Web3 terms are necessary, explain them.
4. **Passionate:** Use emojis sparingly but effectively (🚀, 🎬, 🍿, 💰, 🤖). Show genuine excitement.
5. **Professional yet Warm:** Formal enough for investors, approachable enough for creators.

### 12.2 Key Phrases

- "Defend the Arts" — ecosystem mission
- "Made with ❤️ by YalaCoder" — attribution tagline
- "Decentralized Filmmaker Ecosystem" — descriptor (used in `<title>` and OG tags)
- "IndiFlix" — streaming experience name
- "Indikin Pass" — subscription product name
- "Angel Pass" — lifetime tier name ($999)
- "Stage 1 is SOLD OUT" — used to drive urgency
- "Token Index" — index of bonded filmmaker tokens
- "Creator Hub" — the Discord community name

### 12.3 Meta Description (Canonical)

> "A decentralized filmmaker ecosystem that enables token-based revenue sharing with their communities"

Used in `<meta name="description">`, `og:description`, and `twitter:description`.

### 12.4 Page Title (Canonical)

> "Indikin.online | Decentralized Filmmaker Ecosystem"

---

## 13. Authentication & User Roles

### 13.1 Auth Methods

| Method | Provider | Implementation |
|--------|----------|----------------|
| Email / Password | Firebase Auth | `signInWithEmailAndPassword`, `createUserWithEmailAndPassword` |
| Google OAuth | Firebase Auth (popup/redirect) | `GoogleAuthProvider` via `signInWithPopup` (fallback: `signInWithRedirect`) |
| Discord OAuth | Firebase Auth (popup/redirect) | `OAuthProvider('discord.com')` via `signInWithPopup` (fallback: `signInWithRedirect`) |
| Wallet Connect | MetaMask (ethers.js) | Browser wallet connection on `/login` page |
| Password Reset | Firebase Auth | `sendPasswordResetEmail` with custom action URL `/auth/action` |

### 13.2 User Roles (Firebase Custom Claims)

| Role | Claim Value | Capabilities |
|------|------------|-------------|
| **Admin** | `admin` | Full access: manage films, featured content, users, analytics, admin tools |
| **Filmmaker** | `filmmaker` | Upload films, manage library, AI tools, analytics, trailer management |
| **Filmmaker Basic** | `filmmaker-basic` | Limited filmmaker access (no full filmmaker tools) |
| **Viewer** | `viewer` (default) | Watch content, purchase/redeem passes, manage profile |

Role assignment scripts: `set-admin-claim.cjs`, `set-filmmaker-claim.cjs`, `set-filmmaker-basic-claim.cjs`.

---

## 14. Internationalization (i18n)

- **Library:** `i18next` + `react-i18next`
- **Direction:** Supports LTR and RTL (set via `document.documentElement.dir` on language change)
- **Translations:** JSON files in `src/locales/en/` (English currently; structure supports multiple languages)
- **Usage:** `useTranslation()` hook and `<Trans>` component throughout all UI components
- **RTL-aware CSS:** Classes use `ltr:` and `rtl:` Tailwind variants for directional spacing (e.g., `ltr:mr-2 rtl:ml-2`)

---

## 15. Copyright & Legal

- **Copyright notice:** `© 2025 Indikin.online. All rights reserved.`
- **Code attribution:** Every source file header includes: `© 2025 Indikin.online. All rights reserved. Made with ❤️ by YalaCoder.`
- **Footer credit:** Links to both `indikin.com` and `bitjoinstudios.com`
- **Legal pages:** Privacy Policy, Terms of Service, Cookie Policy — served as Markdown from `public/legal/` with custom `Content-Type: text/markdown; charset=utf-8` header.
- **Cookie consent:** Cookie banner with accept/decline, controlled by `AnalyticsProvider` context.
- **Footer donate CTA:** A donate button that opens the `DonateModal` is present in the footer.
