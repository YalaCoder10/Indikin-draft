# Indikin Architecture Reference

> **For AI Agents:** This file describes the full system architecture, project structure, technology stack, data flow, security model, and deployment topology. Reference this to understand how front-end and back-end interconnect.

---

## 1. System Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         CLOUDFLARE EDGE                            │
│                                                                     │
│  ┌─────────────────────┐     ┌──────────────────────────────────┐  │
│  │  Cloudflare Pages    │     │  Cloudflare Worker (worker.js)    │  │
│  │  ────────────────    │     │  ──────────────────────────────   │  │
│  │  React SPA (Vite)   │────▶│  Serverless API (8346 lines)     │  │
│  │  Static hosting      │     │  REST + Streaming + Webhooks      │  │
│  │  _middleware.js (CSP)│     │  + Cron Scheduled Tasks           │  │
│  └─────────────────────┘     └──────────┬───────────────────────┘  │
│           │                              │                          │
│           │              ┌───────────────┼───────────────────┐      │
│           ▼              ▼               ▼                   ▼      │
│  ┌──────────────┐ ┌───────────┐ ┌─────────────┐ ┌────────────────┐│
│  │CF Stream     │ │CF Images  │ │CF KV Store  │ │CF Analytics    ││
│  │(Video HLS)   │ │(Img CDN)  │ │(Cache/Queue)│ │(GraphQL)       ││
│  └──────────────┘ └───────────┘ └─────────────┘ └────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
        │                                 │
        │                     ┌───────────┴───────────┐
        ▼                     ▼                       ▼
 ┌──────────────┐    ┌──────────────┐       ┌──────────────────┐
 │ Firebase Auth │    │ Firestore DB │       │   3rd-Party APIs │
 │ (JWT + Claims)│    │ (NoSQL)      │       │  ────────────    │
 │               │    │              │       │  Stripe          │
 └──────────────┘    └──────────────┘       │  NOWPayments     │
                                             │  Resend (Email)  │
                                             │  DexScreener     │
                                             │  PulseChain RPC  │
                                             │  Google AI (Gemini)│
                                             └──────────────────┘
```

---

## 2. Front-End Architecture

### 2.1 Technology Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| UI Framework | React | 18.2.0 |
| Build Tool | Vite | 5.4.21 |
| CSS Framework | Tailwind CSS | 3.4.4 |
| Routing | React Router DOM | 6.30.3 (data router / `createBrowserRouter`) |
| State Management | React Context API | 9 providers (no Redux) |
| i18n | i18next + react-i18next | v25 / v15 |
| Forms | Custom (Zod validation) | 3.23.8 |
| Toasts | react-hot-toast | 2.6.0 |
| Carousels | Swiper.js | 12.1.2 |
| Icons | React Icons | 5.2.1 |
| Markdown | react-markdown + remark-gfm | 10.1.0 / 4.0.1 |
| Date Picker | react-datepicker | 7.3.0 |
| Web3 | ethers.js | 6.13.1 |
| Upload | tus-js-client | 4.0.1 |
| Payments | @stripe/react-stripe-js | 2.7.3 |

### 2.2 Directory Structure

```
indikin-online/
├── index.html                 # SPA entry point (shell skeleton + inline critical CSS)
├── package.json               # Dependencies & scripts
├── vite.config.js             # Build config (legacy plugin, inline-css plugin, manual chunks)
├── tailwind.config.js         # Design tokens, fonts, animations
├── postcss.config.cjs         # PostCSS config
├── eslint.config.js           # Linting rules
├── firebase.json              # Firebase hosting config
├── firestore.rules            # Firestore security rules
│
├── public/
│   ├── _headers               # Cloudflare Pages HTTP headers (HSTS, CSP, caching)
│   ├── _routes.json            # Cloudflare Pages routing
│   ├── robots.txt              # SEO robots
│   ├── assets/
│   │   ├── img/               # Logos, heroes, social icons, avatars, covers
│   │   │   ├── logo.png, logo.webp, indikin-logo.svg
│   │   │   ├── hero-bg-{mobile,tablet,desktop}.webp
│   │   │   ├── social-share-card.png
│   │   │   └── {telegram,discord,twitter,...}.{png,webp}
│   │   ├── fonts/             # Self-hosted font files
│   │   └── vids/              # Static video assets
│   ├── data/                  # Public static data files
│   ├── legal/                 # Markdown legal docs (privacy, terms, cookies)
│   ├── lib/                   # Third-party static libraries
│   └── locales/               # Translation JSON (public runtime loading)
│
├── src/
│   ├── main.jsx               # React mount + polyfill imports
│   ├── App.jsx                # Router definition + provider tree + app shell
│   ├── index.css              # Master stylesheet (2072 lines, all design system)
│   ├── i18n.js                # i18next configuration
│   ├── jsconfig.json          # Path alias: @ → ./src
│   │
│   ├── components/
│   │   ├── home/              # 20 homepage section components
│   │   │   ├── Hero.jsx, Hero2.jsx
│   │   │   ├── Ecosystem.jsx, EcosystemComponents.jsx
│   │   │   ├── FoundingFilmmakers.jsx, FoundingFilmmakersCarousel.jsx
│   │   │   ├── FeaturedFilms.jsx, FeaturedFilmsCarousel.jsx
│   │   │   ├── IndikinPass.jsx, IndikinPassCarousel.jsx
│   │   │   ├── RevenueSharing.jsx, NewsletterSignup.jsx
│   │   │   ├── PaymentOptions.jsx, RedeemCodeForm.jsx
│   │   │   ├── WhitelistForm.jsx, FilmmakerCTA.jsx
│   │   │   ├── AnnouncementBanner.jsx
│   │   │   └── cards/         # Sub-card components
│   │   │
│   │   ├── dashboard/
│   │   │   ├── DashboardLayout.jsx, DashboardSidebar.jsx
│   │   │   ├── admin/         # FeaturedFilmsOrder.jsx
│   │   │   ├── filmmaker/     # 16 components (UploadFilm, MyLibrary, Overview, etc.)
│   │   │   ├── viewer/        # 9 components (ViewerDashboard, FilmGrid, etc.)
│   │   │   └── shared/        # Cross-role dashboard components
│   │   │
│   │   ├── layout/            # 11 layout components
│   │   │   ├── Header.jsx, Footer.jsx, MobileMenu.jsx
│   │   │   ├── MainLayout.jsx, AuthLayout.jsx
│   │   │   ├── DashboardLayoutWrapper.jsx
│   │   │   ├── CookieBanner.jsx, LanguageSwitcher.jsx
│   │   │   ├── LegalPage.jsx, SuspenseManager.jsx
│   │   │
│   │   ├── modals/            # 17 modal components
│   │   │   ├── PaymentModal.jsx, IndikinPassModal.jsx
│   │   │   ├── LitepaperModal.jsx, RevenueSharingModal.jsx
│   │   │   ├── BecomeFilmmakerModal.jsx, FilmmakerApplyModal.jsx
│   │   │   ├── VideoPlayerModal.jsx, SetPriceModal.jsx
│   │   │   ├── ShareModal.jsx, WalletModal.jsx
│   │   │   ├── DonateModal.jsx, GlobalAiModal.jsx
│   │   │   ├── ViewerVideoChat.jsx, AnalyticsModal.jsx
│   │   │   ├── AngelPassBenefitsModal.jsx
│   │   │
│   │   ├── shared/            # 20 shared/reusable components
│   │   │   ├── Modal.jsx, ModalLoading.jsx
│   │   │   ├── ProtectedRoute.jsx, ScrollToTop.jsx
│   │   │   ├── GlobalAiButton.jsx, GlobalErrorBoundary.jsx
│   │   │   ├── HeroBackground.jsx, StreamPlayer.jsx
│   │   │   ├── SearchResults.jsx, SocialLoginButtons.jsx
│   │   │   ├── Accordion.jsx, ToggleSwitch.jsx
│   │   │   ├── CarouselArrow.jsx, CarouselPagination.jsx
│   │   │   ├── ImageUpload.jsx, LazyLoad.jsx
│   │   │   ├── PaymentIcons.jsx, ScrollButton.jsx
│   │   │   ├── ResumePrompt.jsx, ConfirmationModal.jsx
│   │   │
│   │   ├── payment/           # Payment flow components
│   │   └── redeem/            # Coupon redemption components
│   │
│   ├── context/               # 16 files (11 providers + 5 context definitions)
│   │   ├── UserProvider.jsx           # Firebase auth state, role claims, profile
│   │   ├── DashboardProvider.jsx      # Films, filmmakers, series, analytics data
│   │   ├── ModalContext.jsx           # Modal open/close state machine
│   │   ├── NavigationProvider.jsx     # Route tracking, scroll state
│   │   ├── WalletContext.jsx          # Ethers.js wallet connection
│   │   ├── AnalyticsProvider.jsx      # Cookie consent, tracking state
│   │   ├── SocialAuthProvider.jsx     # Google + Discord OAuth state
│   │   ├── CarouselProvider.jsx       # Shared carousel state
│   │   ├── GuestUserContext.jsx       # Unauthenticated user state
│   │   └── LoadingProvider.jsx        # Global loading overlay state
│   │
│   ├── hooks/                 # 12 custom hooks
│   │   ├── useUser.js, useAnalytics.js, useLoading.js
│   │   ├── useDashboard.js, useDashboardData.js
│   │   ├── useFilmUploadManager.js    # TUS upload orchestration
│   │   ├── useFilmmakers.js, useFeaturedFilms.js
│   │   ├── useSeries.js, useGridColumns.js
│   │   ├── useGuestUser.js, useSocialAuth.js
│   │
│   ├── services/              # 8 service modules
│   │   ├── api.js             # 50+ API client functions → Worker endpoints
│   │   ├── firebase.js        # Firebase app init, lazy auth
│   │   ├── firestore.js       # Lazy Firestore init
│   │   ├── analytics.js       # Event tracking service
│   │   ├── content.service.js # Content data helpers
│   │   ├── playback.service.js # Stream playback logic
│   │   ├── revenue.service.js # Revenue data helpers
│   │   └── rpcPriceService.js # PulseChain RPC token price fetching
│   │
│   ├── pages/                 # 16 page components
│   │   ├── Home.jsx           # Public homepage (15KB, statically imported)
│   │   ├── Home2.jsx          # Alternative homepage
│   │   ├── Dashboard.jsx      # Protected dashboard
│   │   ├── Login.jsx          # Auth page (email + Google + Discord + wallet)
│   │   ├── Settings.jsx       # User settings & profile
│   │   ├── IndikinPassStatus.jsx # Pass management page
│   │   ├── PublicSharePage.jsx # Public share view (47KB)
│   │   ├── Redeem.jsx         # Coupon redemption page
│   │   ├── FAQ.jsx            # FAQ page
│   │   ├── AuthCallback.jsx, AuthActionHandler.jsx
│   │   ├── PrivacyPolicy.jsx, TermsOfService.jsx, CookiePolicy.jsx
│   │   └── NotFound.jsx       # 404 page
│   │
│   ├── data/                  # Static data
│   │   ├── ecosystem.js       # Token grid (addresses, pairs, images)
│   │   └── faqData.js         # FAQ content
│   │
│   ├── locales/en/            # English translations
│   ├── utils/                 # Utility functions
│   ├── polyfills/             # Legacy browser polyfills
│   └── assets/                # Source assets (bundled by Vite)
│
├── functions/                 # Cloudflare Pages Functions
│   └── _middleware.js         # Dynamic CSP nonce injection
│
├── firebase-functions/        # Firebase Cloud Functions (if any)
├── scripts/                   # Build/deploy scripts
│   └── verify-deps.js        # Dependency security verification
│
├── set-admin-claim.cjs        # Firebase admin claim setter
├── set-filmmaker-claim.cjs    # Filmmaker role claim setter
├── set-filmmaker-basic-claim.cjs # Basic filmmaker claim setter
└── .brand/                    # ← THIS DOCUMENTATION
```

### 2.3 Routing Architecture

Using `createBrowserRouter` (Data Router, React Router v6):

```
Root Element: <AppProviders><AppShell /></AppProviders>
│
├── / (MainLayout)
│   ├── /                     → Home (static import)
│   ├── /home2                → Home2 (lazy)
│   ├── /privacy-policy       → PrivacyPolicy (lazy)
│   ├── /terms-of-service     → TermsOfService (lazy)
│   ├── /cookie-policy        → CookiePolicy (lazy)
│   ├── /redeem               → Redeem (lazy)
│   └── /faq                  → FAQ (lazy)
│
├── (AuthLayout)
│   ├── /login                → Login (lazy)
│   └── /auth/action          → AuthActionHandler (lazy)
│
├── /auth/callback            → AuthCallback (lazy, standalone)
├── /share/:type/:identifier  → PublicSharePage (lazy, standalone)
│
├── (ProtectedRoute → DashboardLayoutWrapper)
│   ├── /dashboard            → Dashboard (lazy)
│   ├── /settings             → Settings (lazy)
│   └── /pass-status          → IndikinPassStatus (lazy)
│
└── *                         → NotFound (lazy)
```

### 2.4 Context Provider Tree (Order Matters)

```
<AnalyticsProvider>
  <UserProvider>                    ← Firebase auth listener
    <GuestUserProvider>
      <SocialAuthProvider>          ← Google + Discord OAuth
        <WalletProvider>            ← Ethers.js
          <NavigationProvider>      ← Route tracking
            <CarouselProvider>
              <LoadingProvider>     ← Global loading
                <ModalProvider>     ← Modal state machine
                  {children}        ← AppShell + Routes
                </ModalProvider>
              </LoadingProvider>
            </CarouselProvider>
          </NavigationProvider>
        </WalletProvider>
      </SocialAuthProvider>
    </GuestUserProvider>
  </UserProvider>
</AnalyticsProvider>
```

> **Note:** `DashboardProvider` is a 10th provider but is **not** in the global tree. It wraps only the dashboard pages (lazy-loaded inside `DashboardLayoutWrapper.jsx`) and manages films, filmmakers, series, and analytics data specific to the dashboard.

### 2.5 Build Configuration Highlights

| Setting | Value | Reason |
|---------|-------|--------|
| `esbuild.target` | `es2017` | Transpile optional chaining for Safari 11 |
| `build.cssCodeSplit` | `false` | Force single CSS file for inline-css plugin |
| `build.minify` | `false` | Currently disabled for debugging |
| Legacy plugin targets | `safari >= 4, ios >= 4` | Extreme backward compatibility |
| Custom inline-css plugin | Inlines CSS into HTML | Eliminates FOUC and CSS loading errors |
| Manual chunks | `vendor-react`, `vendor-stripe`, `vendor-swiper`, `vendor-upload`, `vendor-validation`, `vendor-icons` | Optimized caching strategy |

---

## 3. Back-End Architecture (Worker API)

### 3.1 Technology

- **Runtime:** Cloudflare Workers (V8 isolate)
- **File:** Single `worker.js` (8346 lines, 375KB)
- **Database:** Google Firestore (REST API via custom `Firestore` class)
- **Auth:** Firebase JWT verification (RS256, JWKS from Google)
- **Storage:** Cloudflare KV (caching, queues)
- **Video:** Cloudflare Stream API
- **Images:** Cloudflare Images API
- **Email:** Resend API
- **Payments:** Stripe API, NOWPayments API
- **AI:** Google Gemini API (streaming responses)
- **Blockchain:** PulseChain RPC (ethers-compatible calls)
- **Token Data:** DexScreener API

### 3.2 Worker Config Constants

```js
BRAND_CONFIG = {
  name: "Indikin.online",
  websiteUrl: "https://indikin.online",
  primaryColor: "#FF1493",
  fromEmail: "hello@indikin.online",
  adminEmail: ["info@indikin.com", "indikinonline@gmail.com"],
  logoUrl: "https://indikin.online/assets/img/logo.png",
  socials: [/* 9 platforms */]
}
```

### 3.3 Security Model

1. **CORS:** Strict origin whitelist (`indikin.online`, `*.pages.dev`, `localhost:3000`)
2. **Auth:** Firebase ID token verification on every protected endpoint
3. **Role Claims:** `admin`, `filmmaker`, `filmmaker-basic`, `viewer` (custom Firebase claims)
4. **Video Security:** `requireSignedURLs: true` enforced at creation + verified post-creation (fail-closed)
5. **CSP:** Dynamic nonce-based CSP injected by `_middleware.js`
6. **Headers:** HSTS, X-Frame-Options: DENY, nosniff, strict referrer
7. **Console suppression:** Production builds strip all console.* calls
8. **Service worker cleanup:** Auto-unregisters any rogue service workers
9. **Trusted Types:** Default policy for XSS mitigation

### 3.4 Founding Filmmakers (Hardcoded UIDs)

```js
FOUNDING_FILMMAKER_UIDS = Set([
  'RsdnYvBxmbNwsBQQKhjio5XnV8A3', // Tom Gillespie
  'AaN3yR2WcFg2b4rp3YpZ6zeOhvj2', // Brian
  'QiheLaJFKJOCHuhz0XhFi8avON82', // Georgia
  'MYHkl6RCseQsoaLkoUW68ijnTzu2', // Dr Teed
  '4bq5rCO4ubRunDonajY3ndm2d1A2', // Hal Samples
  'TLCqTiVgCwTWrjVr5WqJxnVd8Sm1', // Bitjoin Studios
])
```

### 3.5 Pass Tiers (Backend-Enforced)

| Tier ID | Price | Name |
|---------|-------|------|
| `stage2` | $99.00 | Stage 2 Indikin Pass |
| `stage3` | $149.00 | Stage 3 Indikin Pass |
| `stage4` | $199.00 | Stage 4 Indikin Pass |
| `stage5` | $249.00 | Stage 5 Indikin Pass |
| `lifetime` | $999.00 | Angel Pass |

> Stage 1 is deprecated and removed.

### 3.6 Cron / Scheduled Tasks

- **Every minute (`* * * * *`):** Payment verification queue processing
- **Every hour (`0 * * * *`):** Email retry queue processing

---

## 4. Data Model (Firestore Collections)

| Collection | Document ID | Key Fields | Purpose |
|-----------|-------------|------------|---------|
| `users` | Firebase UID | `email`, `displayName`, `role`, `passType`, `passExpiry`, `profileImageUrl`, `filmmakerName`, `bio`, `socials` | User accounts |
| `films` | Cloudflare Stream UID | `uid`, `filmmakerUid`, `filmmakerName`, `title`, `description`, `genre`, `releaseDate`, `status`, `uploadType`, `isPublic`, `hasThumbnail`, `seriesId`, `episodeNumber`, `ppvPrice` | Film/video content |
| `series` | UUID | `title`, `filmmakerUid`, `description`, `episodes[]` | Series grouping |
| `subscriptions` | auto | `email`, `type` (`newsletter`/`whitelist`), `createdAt` | Newsletter/whitelist |
| `purchases` | auto | `userId`, `tierId`, `paymentMethod`, `amount`, `status`, `createdAt` | Payment records |
| `featured-films` | film ID | `title`, `filmmakerUid`, `thumbnailUrl`, `trailerUid`, `order` | Homepage featured films |

---

## 5. Ecosystem Token Data

### 5.1 Native Token

```js
{ name: "PulseChain", symbol: "PLS", contractAddress: "0xA1077a294dDE1B09bB078844df40758a5D0f9a27" }
```

### 5.2 Filmmaker Token Index

| Name | Symbol | Contract | Pair |
|------|--------|----------|------|
| INDIKIN INDEX | $INDIKIN | `0xC0372486fCab952aA2B7998876d6aa79d4Fc1938` | `0x2c9596B89c0Ee4b63602Aa789426f7299BDe56dB` |
| SCOOTER COIN | $SCOOT | `0x48792e069CB90d0BEA8b90B85dc6121608611725` | `0xb07B2fa423CebE7C2E8Fa936D099CE083A350E2A` |
| GORGE PUKAS | $WUPIUPI | `0x12B3E0d79c5dFda3FfA55D57C9697bD509dBf7B0` | `0x1E29552D159F4417b77e8a6120C9Cd19617D88C7` |
| LOLA HEART | $LOLA | `0x99FE558cC0f80542EFeEa74a3B6f827c8452308E` | `0x5048ec04747CcD2B93095CB9E9D9cFBc5CA6028D` |
| DR TEED | $TEED | `0xa55385633fffab595e21880ed7323cfd7d11cd25` | `0xB4575B7d41d1b94957238B4Ac591fA82ac1960Ae` |
| TOM GILLESPIE | $GDAY | `0x3981920A82d95A117A8747eCF9A11e105Ca38B62` | `0xB2A40341C81CBa0811386d821CFfe49929E7ac4F` |
| HAL SAMPLES | $HAL | `0x9304Bb4931C8A004d8d078402D9b99C0ae895043` | `0x9D6Ab51f15ceAbD1BD9B6446bb8517ef6892e5B1` |
| BAAANA MASSIK | $BAANA | `0x637Ecd6b33BD8d5A550939A2e6058Dd7Dc52812e` | `0x592C495AAf8649eaB16670CcC4354c3B6b3fD14e` |

---

## 6. Deployment

### 6.1 Front-End (Cloudflare Pages)

- **Build command:** `npm run build`
- **Output directory:** `dist/`
- **Branch:** main
- **Environment variables:** `VITE_FIREBASE_*`, `VITE_API_BASE_URL`
- **Middleware:** `functions/_middleware.js` (dynamic CSP nonce injection)

### 6.2 Back-End (Cloudflare Workers)

- **File:** `worker.js` (single file deployment)
- **KV Namespaces:** Cache store, verification queue
- **Environment bindings:** Firebase service account keys, Stripe secret, NOWPayments key, CF account/tokens, Resend key, Gemini key
- **Cron triggers:** `* * * * *` (per-minute), `0 * * * *` (hourly)
- **Custom domains:** API served from Worker routes

### 6.3 Production URLs

| Service | URL |
|---------|-----|
| Front-end | `https://indikin.online` / `https://www.indikin.online` |
| Back-end API | Worker route (same or custom domain) |
| Staging | `https://indikin-online.pages.dev` |
| Dev server | `http://localhost:3000` |
