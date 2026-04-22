# Indikin `.brand/` Documentation Index

> **For AI Agents:** Read this file first. It tells you which file to consult for any given question about the Indikin project.

---

## Files in This Directory

| File | Lines | What It Answers |
|------|-------|-----------------|
| [BRAND_IDENTITY.md](./BRAND_IDENTITY.md) | ~465 | Mission, vision, tagline, brand hierarchy, pass tiers, logo assets (20+), full color palette (13 CSS tokens), typography (Inter+Montserrat via Google Fonts CDN), iconography, hero backgrounds with app shell skeleton, video platform details, all 16 animations, spacing/layout, 11 social channels (incl. Clubhouse & Bluesky), tone of voice with canonical meta descriptions, 4 auth methods (email/Google/Discord/wallet), 4 user roles, i18n/RTL support, copyright & legal. |
| [DESIGN_SYSTEM.md](./DESIGN_SYSTEM.md) | ~458 | Every CSS custom property, Tailwind color alias + custom maxWidth + typography plugin, heading selectors with @layer note, button variants (7 types), card patterns (base/pass/film/filmmaker), form/modal/header/hero/section styles, 3 swiper configs with verified dimensions (film: 320px/1.05, filmmaker: 340px/1.0, tier: 360px/0.85), gradient border (1px mask composite), shine/typing/cookie/sold-out/live effects. |
| [ARCHITECTURE.md](./ARCHITECTURE.md) | ~430 | System topology diagram, full technology stack, directory tree (130+ files mapped), React Router route table, Context provider tree (9 global + 1 lazy dashboard), Vite build config, Worker API architecture (8346 lines), security model (9 layers), Founding Filmmaker UIDs, Firestore data model (6 collections), PulseChain ecosystem tokens (8 entries), deployment topology. |
| [API_REFERENCE.md](./API_REFERENCE.md) | ~270 | All 50+ Worker API endpoints grouped by 16 domains (user, payments×3, coupons, films, subtitles, series, featured, tokens, AI chat, analytics, public/sharing, social redirects, admin, webhooks). Method, path, auth requirement, description. Front-end API client pattern. Error response format. |

---

## Quick Decision Guide

| If you need to… | Read… |
|-----------------|-------|
| Match brand colors/fonts | `BRAND_IDENTITY.md` §4-5 |
| Write a new CSS component | `DESIGN_SYSTEM.md` §4-9 |
| Add a new page/route | `ARCHITECTURE.md` §2.3 |
| Add a new context provider | `ARCHITECTURE.md` §2.4 |
| Call or add an API endpoint | `API_REFERENCE.md` §4 |
| Understand Firestore schema | `ARCHITECTURE.md` §4 |
| Write copy/marketing | `BRAND_IDENTITY.md` §12 |
| Check deployment config | `ARCHITECTURE.md` §6 |
| Work with ecosystem tokens | `ARCHITECTURE.md` §5 |
| Understand security model | `ARCHITECTURE.md` §3.3 |
| Understand auth methods/roles | `BRAND_IDENTITY.md` §13 |
| Add i18n / RTL support | `BRAND_IDENTITY.md` §14 |
| Build a new swiper/carousel | `DESIGN_SYSTEM.md` §9 |
| Understand gradient borders | `DESIGN_SYSTEM.md` §10 |
