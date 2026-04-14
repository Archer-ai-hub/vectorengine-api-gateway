# Vector Engine API Gateway

[![Gitee](https://img.shields.io/badge/Gitee-VectorEngine--API--网关-C71D23?style=flat-square)](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关)
[![GitHub mirror](https://img.shields.io/badge/GitHub-mirror-181717?style=flat-square&logo=github)](https://github.com/Archer-ai-hub/vectorengine-api-gateway)
[![Console](https://img.shields.io/badge/Console-api.vectorengine.ai-0284c7?style=flat-square)](https://api.vectorengine.ai/)
[![Apifox](https://img.shields.io/badge/API%20catalog-Apifox-7c3aed?style=flat-square)](https://vectorengine.apifox.cn/)
[![English guide](https://img.shields.io/badge/docs-English%20integration-16a34a?style=flat-square)](#documentation--links)
[![Telegram](https://img.shields.io/badge/Telegram-@ZXCZCI-0088cc?style=flat-square)](https://t.me/ZXCZCI)

**This repo (Gitee):** [gitee.com/弓箭手-艾-hub/VectorEngine-API-网关](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关) · **Mirror (GitHub):** [Archer-ai-hub/vectorengine-api-gateway](https://github.com/Archer-ai-hub/vectorengine-api-gateway)

> **High-performance AI API access layer for [Vector Engine](https://api.vectorengine.ai/) — OpenAI-compatible calls, unified wallet & keys, and a large multi-vendor model catalog for builders who ship real products.**

**简体中文（摘要）：** 本仓库说明 **Vector Engine（矢量引擎）** 的 API 网关与控制台入口；**正文以英文为主**，便于海外开发者阅读。产品控制台支持多语言切换。

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

## Quick start (first chat call)

1. [Register / sign in](https://api.vectorengine.ai/) → **Model Square** → pick **model id** + **group** → **API Token** → create a key with that **same group**.  
2. In [Apifox](https://vectorengine.apifox.cn/), copy the **Server / Base URL** for your environment (often like `https://api.vectorengine.ai/v1` — **verify live**).  
3. Run (replace placeholders):

```bash
export VECTOR_ENGINE_BASE_URL="https://api.vectorengine.ai/v1"   # confirm in Apifox
export VECTOR_ENGINE_API_KEY="sk-..."                            # your console token
export VECTOR_ENGINE_MODEL="YOUR_SITE_MODEL_ID"                  # from Model Square

curl -sS "${VECTOR_ENGINE_BASE_URL}/chat/completions" \
  -H "Authorization: Bearer ${VECTOR_ENGINE_API_KEY}" \
  -H "Content-Type: application/json" \
  -d "{\"model\":\"${VECTOR_ENGINE_MODEL}\",\"messages\":[{\"role\":\"user\",\"content\":\"Hello\"}]}"
```

```python
from openai import OpenAI
import os

client = OpenAI(
    api_key=os.environ["VECTOR_ENGINE_API_KEY"],
    base_url=os.environ["VECTOR_ENGINE_BASE_URL"],
)
r = client.chat.completions.create(
    model=os.environ["VECTOR_ENGINE_MODEL"],
    messages=[{"role": "user", "content": "Hello"}],
)
print(r.choices[0].message.content)
```

**403 / 401?** Re-check **URL path**, **key group**, and **`model`** string — see [Integration at a glance](#integration-at-a-glance).

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

- **Star** on [Gitee](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关) (or [GitHub mirror](https://github.com/Archer-ai-hub/vectorengine-api-gateway)) — helps others find this doc.  
- **Share** with your team’s platform / backend channel.  
- **Issues:** [Gitee Issues](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关/issues) · [GitHub Issues (mirror)](https://github.com/Archer-ai-hub/vectorengine-api-gateway/issues) for doc/link fixes.

---

## Updates

| Date       | Notes |
|------------|--------|
| 2026-04    | README refresh: international layout, optional entry host wording, operator entity. |

---

## Table of contents

- [Quick start (first chat call)](#quick-start-first-chat-call)
- [Quick reference](#quick-reference)
- [What is Vector Engine API Gateway?](#what-is-vector-engine-api-gateway)
- [API entry points](#api-entry-points)
- [Who this is for](#who-this-is-for)
- [Console highlights](#console-highlights)
- [Integration at a glance](#integration-at-a-glance)
- [Documentation & links](#documentation--links)
- [Contact (primary & backup)](#contact-primary--backup)
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
| **Human support** | **Primary:** Telegram [@ZXCZCI](https://t.me/ZXCZCI) · **Backup:** [yeallen441@gmail.com](mailto:yeallen441@gmail.com?subject=Vector%20Engine%20API%20support) |

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
| **This repo (Gitee)** | [gitee.com/弓箭手-艾-hub/VectorEngine-API-网关](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关) |
| **Mirror (GitHub)** | [github.com/Archer-ai-hub/vectorengine-api-gateway](https://github.com/Archer-ai-hub/vectorengine-api-gateway) |
| **Integration guide (Markdown)** | [docs/INTEGRATION.md](docs/INTEGRATION.md) |
| **Env template (no secrets)** | [examples/.env.example](examples/.env.example) |
| Web console | [https://api.vectorengine.ai/](https://api.vectorengine.ai/) |
| Apifox (API catalog) | [https://vectorengine.apifox.cn/](https://vectorengine.apifox.cn/) |
| Register (affiliate promo; bonus credits when rules apply) | [https://api.vectorengine.ai/register?aff=prKT](https://api.vectorengine.ai/register?aff=prKT) |
| Telegram (primary) | [https://t.me/ZXCZCI](https://t.me/ZXCZCI) |
| Email (backup) | [yeallen441@gmail.com](mailto:yeallen441@gmail.com?subject=Vector%20Engine%20API%20support) |
| Gitee Issues (docs / links) | [Issues](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关/issues) |
| GitHub Issues (mirror) | [Issues](https://github.com/Archer-ai-hub/vectorengine-api-gateway/issues) |

**Optional:** enable **Gitee Pages** or **GitHub Pages** on `main` → `/docs` to render Markdown in browser, or add your long-form English HTML under `docs/` and link it here.

---

## Contact (primary & backup)

| Priority | Channel | Use for |
|----------|---------|---------|
| **1** | Telegram [@ZXCZCI](https://t.me/ZXCZCI) | Fastest: onboarding, billing, USDT, `aff=prKT`, which group to pick. |
| **2** | [yeallen441@gmail.com](mailto:yeallen441@gmail.com?subject=Vector%20Engine%20API%20support) | Same as above if you cannot use Telegram; **do not** send `sk-` API keys. |
| **3** | [Gitee Issues](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关/issues) · [GitHub (mirror)](https://github.com/Archer-ai-hub/vectorengine-api-gateway/issues) | README / doc typos, broken links — not for account-specific support. |

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

This repository’s **documentation and examples** are licensed under the [MIT License](LICENSE).  
The **Vector Engine hosted service** and third-party models remain under their own terms — see the license file scope note.

---

## Maintainer checklist (Gitee / GitHub settings)

Things README alone cannot fix — worth doing on [Gitee](https://gitee.com/弓箭手-艾-hub/VectorEngine-API-网关) and/or [GitHub mirror](https://github.com/Archer-ai-hub/vectorengine-api-gateway):

| Item | Why |
|------|-----|
| **About → Description** | Keep one crisp English line (already good) — matches global search. |
| **About → Website** | Set to `https://api.vectorengine.ai` so the sidebar links to the product. |
| **Topics / tags** | e.g. `openai-api`, `llm`, `api-gateway`, `vector-engine`, `multimodal`, `ai` — improves discovery. |
| **README 结构** | **只保留一个一级标题 `#`**；不要同时存在 `# vectorengine-api-gateway` 与 `# Vector Engine API Gateway` 两个并列大标题。 |
| **不要嵌套整包文件夹** | 不要把 ZIP 解压后的内容再套一层 `vectorengine-api-gateway-UPLOAD/` 上传 — 应把 `docs/`、`examples/` 等放在**仓库根目录**。 |
| **`LICENSE`** | ✅ Added [`LICENSE`](LICENSE) (MIT + hosted-service scope note). Change if legal prefers proprietary docs only. |
| **Releases or tags** | Publish **`v0.1.0`** — step-by-step: [`RELEASING.md`](RELEASING.md) · history: [`CHANGELOG.md`](CHANGELOG.md). |
| **SECURITY.md** | ✅ [`SECURITY.md`](SECURITY.md) — includes **mailto:yeallen441@gmail.com** for disclosures. |

---

*Vector Engine API Gateway README — structured for international developers; keep the quick reference table in sync with the live product.*
