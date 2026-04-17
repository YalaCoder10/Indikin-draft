# Indikin API Reference

> **For AI Agents:** This file documents every API endpoint exposed by the Worker back-end (`worker.js`). Use this to understand request/response contracts when building or modifying front-end features.

---

## 1. Base URL

```
Production:  Cloudflare Worker route (configured via VITE_API_BASE_URL)
Development: http://127.0.0.1:8788
```

All requests use JSON bodies (`Content-Type: application/json`) unless noted otherwise.

## 2. Authentication

Protected endpoints require a Firebase ID token in the `Authorization` header:

```
Authorization: Bearer <firebase_id_token>
```

The Worker verifies the JWT against Google's JWKS endpoint and extracts:
- `uid` — Firebase user ID
- `role` — Custom claim (`admin`, `filmmaker`, `filmmaker-basic`, `viewer`)

---

## 3. CORS

Allowed origins: `indikin.online`, `www.indikin.online`, `indikin-online.pages.dev`, `localhost:3000`, `127.0.0.1:3000`.

Preflight `OPTIONS` requests are handled automatically.

---

## 4. Endpoint Reference

### 4.1 User & Profile

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/subscribe` | Optional | Subscribe to newsletter |
| `POST` | `/whitelist` | Optional | Submit whitelist application |
| `POST` | `/filmmaker-apply` | Optional | Submit filmmaker application |
| `GET` | `/filmmakers?_t={timestamp}` | Optional | Get all filmmakers list |
| `POST` | `/user/welcome-email` | ✅ | Trigger welcome email |
| `GET` | `/user-pass-status` | ✅ | Get user's pass/subscription status |
| `GET` | `/user-purchases` | ✅ | Get user's purchase history |
| `POST` | `/gift-pass` | ✅ | Gift a pass to another user |
| `DELETE` | `/user/delete` | ✅ | Delete user account |
| `PATCH` | `/user/profile` | ✅ | Update user profile (displayName, bio, socials) |
| `POST` | `/user/profile/image-upload` | ✅ | Request Cloudflare Images direct upload URL |

### 4.2 Payments — Stripe

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/stripe/create-payment-intent` | ✅ | Create Stripe payment intent for pass purchase |
| `POST` | `/stripe/create-tip-intent` | No | Create Stripe payment intent for tipping |
| `POST` | `/stripe-webhook` or `/stripe/webhook` | No (Stripe sig) | Stripe webhook handler |

### 4.3 Payments — NOWPayments (Crypto)

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `GET` | `/get-available-currencies` | ✅ | List supported NOWPayments currencies |
| `GET` | `/get-fiat-estimate` | ✅ | Get fiat-to-crypto estimate |
| `POST` | `/create-payment-invoice` | ✅ | Create NOWPayments invoice |
| `GET` | `/payment-status?orderId={id}` | ✅ | Check payment status |
| `POST` | `/nowpayments-ipn` | No (IPN sig) | NOWPayments webhook (IPN) |
| `GET` | `/pending-payment-details?orderId={id}` | ✅ | Get pending payment details |
| `POST` | `/redeem-resume-token` | Optional | Redeem payment resume token |

### 4.4 Payments — Native Crypto (PulseChain)

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/init-crypto-payment` | ✅ | Initiate native crypto payment |
| `GET` | `/get-public-balance?wallet={addr}&token={addr}` | ✅ | Get public wallet balance |
| `POST` | `/verify-crypto-payment` | ✅ | Verify on-chain crypto payment |
| `GET` | `/check-wallet-email?wallet={addr}` | No | Check if wallet has associated email |

### 4.5 Coupons

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/redeem-coupon` | ✅ | Redeem a coupon code |

### 4.6 Film & Video Management

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/initiate-url-upload` | ✅ | Ingest film from public URL (Cloudflare Stream copy) |
| `POST` | `/create-direct-upload-film-document` | ✅ | Create Firestore film doc for TUS upload |
| `POST` | `/request-direct-upload` | ✅ | Request TUS upload URL from Cloudflare Stream |
| `PATCH` | `/film/{filmId}` | ✅ | Update film metadata |
| `POST` | `/film/{filmId}` | ✅ | Check film processing status |
| `DELETE` | `/film/{filmId}` | ✅ | Delete film |
| `GET` | `/film/{filmId}/status` | ✅ | Poll upload/processing status |
| `POST` | `/film/{filmId}/request-thumbnail-upload` | ✅ | Request thumbnail upload URL |
| `POST` | `/stream/{uid}/token` | ✅ | Generate signed playback token |
| `GET` | `/thumbnail/{uid}` | No | Proxy thumbnail image (cached) |
| `*` | `/tus-proxy/{videoId}` | Varies | TUS protocol proxy to Cloudflare Stream |

### 4.7 Subtitles & AI Captions

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `PUT` | `/film/{filmId}/subtitle/{language}` | ✅ | Upload VTT subtitle file (multipart) |
| `GET` | `/film/{filmId}/subtitle/{language}/download` | ✅ | Download existing subtitle |
| `DELETE` | `/film/{filmId}/subtitle/{subtitleId}` | ✅ | Delete subtitle |
| `POST` | `/film/{filmId}/captions/generate` | ✅ | Generate AI captions (Cloudflare Stream AI) |
| `GET` | `/film/{filmId}/captions/draft-status?language={lang}` | ✅ | Poll AI caption generation status |

### 4.8 Series Management

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/series` | ✅ | Create new series |
| `PATCH` | `/series/{seriesId}` | ✅ | Update series metadata |

### 4.9 Featured Films (Admin/Founding Filmmaker)

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `GET` | `/featured-films` | No | Get featured films list |
| `POST` | `/featured-films/request-upload` | ✅ | Request trailer upload URL |
| `POST` | `/featured-films/request-thumbnail-upload` | ✅ | Request featured thumbnail upload |
| `PATCH` | `/featured-films/update` | ✅ | Update featured film metadata |
| `PATCH` | `/featured-films/reorder` | ✅ | Reorder featured films |
| `DELETE` | `/featured-films/delete` | ✅ | Delete featured film |

### 4.10 Token & Price Data

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/token-data` | Optional | Batch fetch token data from DexScreener |
| `GET` | `/get-token-price?address={}&pairAddress={}&isNative={}` | Optional | Get single token price (RPC + DexScreener) |

### 4.11 AI Chat (Streaming)

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/ai/filmmaker-chat` | ✅ | AI brainstorming chat for filmmakers (SSE stream) |
| `POST` | `/ai/video-chat` | ✅ | Context-aware AI chat while watching video (SSE stream) |

### 4.12 Analytics

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `GET` | `/analytics/summary` | ✅ | Filmmaker analytics summary (30-day + all-time) |
| `GET` | `/analytics/summary/daily` | ✅ | Daily analytics summary |
| `POST` | `/analytics/content` | ✅ | Per-content analytics for specific UIDs |
| `GET` | `/analytics/content-summary` | ✅ | Aggregate per-content analytics summary |

### 4.13 Public & Sharing

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `GET` | `/public/share/{type}/{identifier}` | No | Public share data (film/series/filmmaker by slug or ID) |
| `GET` | `/sitemap.xml` | No | Dynamic sitemap generation |
| `GET` | `/qr-code` | No | QR code generation |

### 4.14 Social Redirects

| Path | Redirects To |
|------|-------------|
| `/social/telegram` | `https://t.me/+uC-rKNh6BFw3MzI8` |
| `/social/discord` | `https://discord.gg/3CnX4F3QkY` |
| `/social/twitter` | `https://x.com/IndiKinofficial` |
| `/social/youtube` | `https://www.youtube.com/@IndiKin` |
| `/social/reddit` | `https://www.reddit.com/r/indikin` |
| `/social/linkedin` | `https://www.linkedin.com/showcase/indikin` |
| `/social/facebook` | `https://www.facebook.com/indikinofficial` |
| `/social/tiktok` | `https://www.tiktok.com/@indikinofficial` |
| `/social/instagram` | `https://www.instagram.com/indikinofficial` |

### 4.15 Admin & Migration

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/admin/migrate-thumbnails` | ✅ (admin) | Batch migrate thumbnails |
| `POST` | `/admin/enforce-security` | ✅ (admin) | Enforce security settings on all videos |

### 4.16 Webhooks & System

| Method | Path | Auth | Description |
|--------|------|------|-------------|
| `POST` | `/stream-webhook` | CF sig | Cloudflare Stream status webhook |
| `POST` | `/beacon` | No | Analytics beacon endpoint |
| `GET` | `/check-whitelist` | No | Check whitelist status |
| `GET` | `/unsubscribe` | No | Email unsubscribe handler |
| `GET` | `/auth/callback` | No | OAuth callback handler |
| `GET` | `/export` | ✅ (admin) | Export data |
| `GET` | `/debug-secrets` | ✅ (admin) | Debug environment bindings |

---

## 5. Front-End API Client

All API calls are centralized in `src/services/api.js`:

```js
import { API_BASE_URL } from '@/services/api';

// Pattern: every function calls `apiFetch(endpoint, options, idToken)`
// apiFetch handles:
//   - Base URL joining
//   - Content-Type headers
//   - Authorization header injection
//   - JSON parsing
//   - Error handling with backend message extraction
```

### Usage Pattern (from Components/Hooks)

```jsx
import { useUser } from '@/hooks/useUser';
import { getFilmmakers } from '@/services/api';

// Inside component:
const { getIdToken } = useUser();
const token = await getIdToken();
const data = await getFilmmakers(token);
```

---

## 6. Error Response Format

All errors return JSON:

```json
{
  "message": "Human-readable error description"
}
```

HTTP status codes follow REST conventions:
- `400` — Bad request / validation error
- `401` — Unauthorized (missing/invalid token)
- `403` — Forbidden (insufficient role)
- `404` — Endpoint not found
- `405` — Method not allowed
- `500` — Internal server error
- `502` — Bad gateway (upstream API failure)
