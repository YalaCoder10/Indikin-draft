# Indikin Technical Development (6)

> **For AI Agents:** This directory houses the definitive technical specifications for the Indikin platform. Reference these files for all code generation, UI development, and architectural decisions.

---

## Technical Domain Index

| If you need to... | Read... | Section |
|-------------------|---------|---------|
| Match brand colors/fonts | [BRAND_IDENTITY.md](./BRAND_IDENTITY.md) | §4-5 |
| Build a new UI component | [DESIGN_SYSTEM.md](./DESIGN_SYSTEM.md) | §4-9 |
| Understand system topology | [ARCHITECTURE.md](./ARCHITECTURE.md) | §1 |
| Map Firestore collections | [ARCHITECTURE.md](./ARCHITECTURE.md) | §4 |
| Call or add an API endpoint | [API_REFERENCE.md](./API_REFERENCE.md) | §4 |
| Check deployment configs | [ARCHITECTURE.md](./ARCHITECTURE.md) | §6 |

---

## Engineering Stack
- **Frontend**: React (Vite) + Tailwind CSS + Ethers.js
- **Backend**: Cloudflare Workers (Single-file serverless API)
- **Database**: Google Firestore (NoSQL)
- **Video/Media**: Cloudflare Stream & Images

## Important Note on Assets
> [!NOTE]
> High-resolution brand assets (logos, SVG icons, and raw backgrounds) are maintained in the primary **codebase repository** under `public/assets/img/`. This documentation provides the logical specifications and CSS tokens for their implementation.

---

## AI Agent Integration
The technical foundation supports the autonomous operation of the Indikin Agent Suite. Specific endpoint permissions and data models for **DEVA**, **MODRA**, and **ONBA** are detailed in the [API_REFERENCE.md](./API_REFERENCE.md).
