# vectorengine-api-gateway
High-speed AI API proxy &amp; gateway service for VectorEngine, enabling stable, low-latency access to global large language models.
# Vector Engine API Gateway

[![GitHub stars](https://img.shields.io/github/stars/Archer-ai-hub/vectorengine-api-gateway?style=social)](https://github.com/Archer-ai-hub/vectorengine-api-gateway)
[![Repo](https://img.shields.io/badge/GitHub-Archer--ai--hub%2Fvectorengine--api--gateway-181717?style=flat-square&logo=github)](https://github.com/Archer-ai-hub/vectorengine-api-gateway)
[![Console](https://img.shields.io/badge/Console-api.vectorengine.ai-0284c7?style=flat-square)](https://api.vectorengine.ai/)
[![Apifox](https://img.shields.io/badge/API%20catalog-Apifox-7c3aed?style=flat-square)](https://vectorengine.apifox.cn/)
[![English guide](https://img.shields.io/badge/docs-English%20integration-16a34a?style=flat-square)](#documentation--links)
[![Telegram](https://img.shields.io/badge/Telegram-@ZXCZCI-0088cc?style=flat-square)](https://t.me/ZXCZCI)

**Repository:** [github.com/Archer-ai-hub/vectorengine-api-gateway](https://github.com/Archer-ai-hub/vectorengine-api-gateway) · edit README on GitHub: [README.md (main)](https://github.com/Archer-ai-hub/vectorengine-api-gateway/edit/main/README.md)

> **High-performance AI API access layer for [Vector Engine](https://api.vectorengine.ai/) — OpenAI-compatible calls, unified wallet & keys, and a large multi-vendor model catalog for builders who ship real products.**

### What's inside

- ✅ **OpenAI-compatible** HTTP surface for many LLM & multimodal SKUs  
- ✅ **One console** — Model Square, token **groups** bound per API key, usage & billing  
- ✅ **Global-friendly UI** — English plus Chinese, Russian, Korean, Japanese, Spanish, German  
- ✅ **Flexible top-up** — USDT, Alipay, WeChat Pay, redemption codes (as shown in **Wallet**)  
- ✅ **Documented routes** — request/response detail in **Apifox**  
- ✅ **Optional entry host** for routing / redundancy (same account & keys as primary)

**Goal:** Give developers **stable, low-latency** access to global and domestic models through **one integration pattern** (URL + Bearer key + `model` id), without juggling a dozen vendor dashboards.

> [!NOTE]  
> **Live data wins.** Model lists, multipliers, and prices change often. Always verify **Model Square**, **Wallet**, and **Apifox** after you read this README.

> [!WARNING]  
> **Keys are secrets.** Never commit API tokens; use env vars and a backend proxy for public apps.

---

## Why this repository exists

Many “API gateway” repos are either:

- ❌ A thin reverse proxy with no explanation of **billing, groups, or model IDs**  
- ❌ Abandoned configs from 2023  
- ❌ Opaque scripts with no link to an **authoritative HTTP contract**

**This repo is for:**

- ✅ Operators & integrators who want **clear entry points** and **operational context** for Vector Engine’s gateway  
- ✅ Teams that already use **OpenAI SDKs** and want to swap `base_url` + key  
- ✅ Anyone who needs **one place** to point new hires: console, Apifox, support

**This is not:** a replacement for Apifox (schemas live there) or the logged-in console (balances and keys live there).

---

## Star & share

If this README saved you a debugging afternoon:

- **[Star this repo](https://github.com/Archer-ai-hub/vectorengine-api-gateway)** — helps others discover Vector Engine gateway notes.  
- **Share** with your team’s platform / backend channel.  
- **[Open an issue](https://github.com/Archer-ai-hub/vectorengine-api-gateway/issues)** if an entry point, mirror host, or doc link drifts — we’ll align the table.

---

## Updates

| Date       | Notes |
|------------|--------|
| 2026-04    | README refresh: international layout, optional entry host wording, operator entity. |

---

## Table of contents

- [Quick reference](#quick-reference)
- [What is Vector Engine API Gateway?](#what-is-vector-engine-api-gateway)
- [API entry points](#api-entry-points)
- [Who this is for](#who-this-is-for)
- [Console highlights](#console-highlights)
- [Integration at a glance](#integration-at-a-glance)
- [Documentation & links](#documentation--links)
- [Operator & legal](#operator--legal)
- [Contributing](#contributing)
- [License](#license)

---

## Quick reference

| Topic | Where to look |
|--------|----------------|
| **Sign in / register** | [api.vectorengine.ai](https://api.vectorengine.ai/) |
| **Model + group (price tier)** | Console → **Model Square** → **Group pricing** (分组价格) |
| **Create API key** | Console → **API Token** / **API Keys** → assign **group** to match Model Square |
| **HTTP schemas & try-it** | [vectorengine.apifox.cn](https://vectorengine.apifox.cn/) |
| **Top up** | Console → **Personal Center → Wallet** (USDT / Alipay / WeChat / codes) |
| **Human support** | Telegram [@ZXCZCI](https://t.me/ZXCZCI) |

---

## What is Vector Engine API Gateway?

**Vector Engine** is a **managed AI API platform**: we aggregate hundreds of **LLM and multimodal** SKUs behind a coherent **console + billing** experience. Your application calls our **HTTP API** (often **OpenAI-compatible** for chat) using:

1. A **base URL** we document per product line (see Apifox).  
2. A **Bearer token** issued in the console.  
3. The exact **`model`** string from **Model Square** for that key’s scope.

**Groups** (令牌分组) are **not** sent as an extra header — the **group is selected when the key is created** and drives routing and **credit** burn.

---

## API entry points

| Host | Role |
|------|------|
| **`https://api.vectorengine.ai`** | **Primary** API entry — main integration host; document paths & base URL in Apifox. |
| **`https://api.zhongzhuan.vip`** | **Optional** alternate API host on the **same platform** as `api.vectorengine.ai` — same account, wallet balance, and API tokens; for **routing choice and redundancy**. Paths, `Authorization`, and billing match the primary site. **Not** a no-login or billing-free bypass. |

Use the host your team standardizes on; confirm **latency and availability** from your region. When in doubt, prefer the **primary** host unless operations or support specifies the alternate.

---

## Who this is for

| Audience | Why |
|----------|-----|
| **Backend / platform engineers** | One integration style; Apifox as contract. |
| **IDE & agent users** | Cursor-style clients: set `base_url` + model id from Model Square. |
| **Global + CN stacks** | Mixed vendors, one wallet and catalog. |
| **Automation & media pipelines** | Chat + image / video / audio routes (per Apifox). |

---

## Console highlights

- **Languages:** header language switcher — **English**, **Chinese**, **Russian**, **Korean**, **Japanese**, **Spanish**, **German** (a few labels may still mix during polish).  
- **Wallet:** **Alipay**, **WeChat Pay**, **USDT**, **redemption code** top-up — whatever the live checkout shows.  
- **Dashboard:** API panel lists **primary** (and optionally **alternate**) base URLs for quick copy / speed tests.

---

## Integration at a glance

1. Pick model + **group** row in **Model Square**.  
2. Create an API key with the **same group** name.  
3. Call the **documented URL** + send `Authorization: Bearer <key>` + correct **`model`**.  

If you see **401 / 403 / model not allowed**, re-check **URL path**, **key’s group**, and **`model`** string — in that order.

---

## Documentation & links

| Resource | Link |
|----------|------|
| **This GitHub repo** | [github.com/Archer-ai-hub/vectorengine-api-gateway](https://github.com/Archer-ai-hub/vectorengine-api-gateway) |
| Web console | [https://api.vectorengine.ai/](https://api.vectorengine.ai/) |
| Apifox (API catalog) | [https://vectorengine.apifox.cn/](https://vectorengine.apifox.cn/) |
| Register (affiliate promo; bonus credits when rules apply) | [https://api.vectorengine.ai/register?aff=prKT](https://api.vectorengine.ai/register?aff=prKT) |
| Telegram (onboarding / billing) | [https://t.me/ZXCZCI](https://t.me/ZXCZCI) |

Add a **long-form English integration** doc (HTML/Markdown) in this repo or enable **GitHub Pages**, then link it here for a single-scroll onboarding page.

---

## Operator & legal

**Chongqing Ruize Zhijie Technology Co., Ltd.**  
重庆瑞泽智界科技有限公司  

The logged-in console footer links to the current **Privacy Policy** and related notices. **Invoice / billing record** availability follows what the **Wallet** and order UI allows for your account.

---

## Contributing

PRs welcome for:

- Fixing broken links or outdated tables in this README  
- Adding deployment examples (env samples only — **no real keys**)

---

## License

Specify your license in this repository’s `LICENSE` file (e.g. MIT). Until then, **code** defaults to “all rights reserved” unless you state otherwise.

---

*Vector Engine API Gateway README — structured for international developers; keep the quick reference table in sync with the live product.*
