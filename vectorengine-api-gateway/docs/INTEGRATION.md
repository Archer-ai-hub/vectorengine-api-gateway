# Vector Engine — integration guide (concise)

English · for developers integrating the **HTTP API**. Authoritative request/response detail: **[Apifox](https://vectorengine.apifox.cn/)**. Live catalog and billing: **[Console](https://api.vectorengine.ai/)**.

---

## 1. Triple match (must hold on every call)

| Piece | Where you get it |
|--------|-------------------|
| **Request URL** | Host + path documented for that SKU (OpenAI-style chat, or e.g. `/mj/…`, `/kling/…`). |
| **API key** | Console → **API Token** — created with a **group** that matches Model Square. |
| **`model`** | Exact **site model id** from **Model Square** (same row / group you chose). |

The **group** is **not** an extra HTTP header — it is selected when the key is created.

---

## 2. End-to-end flow

1. **Model Square** — pick model → note **model id** + **API endpoint** block.  
2. **Group pricing** (分组价格) — pick the **group** row (price / route tier).  
3. **API Token** — create key with **the same group name**.  
4. **Call** — documented base URL + `Authorization: Bearer <key>` + body with that **`model`**.

---

## 3. Base URL

Copy **Server / Base URL** from your Apifox environment. A common pattern is `https://api.vectorengine.ai/v1` — **verify before production**.

Optional alternate host (same account & keys): `https://api.zhongzhuan.vip` — same paths and billing rules as the primary host; not a no-login bypass.

---

## 4. Model Square filter numbers (console)

- **可用令牌分组** chips show **×N** = **billing multiplier** for that group (not “number of models”).  
- **供应商 / 模型类型 / 标签 / 计费类型** etc. — numbers are **catalog counts** (how many SKUs match).

---

## 5. Auth header

```http
Authorization: Bearer sk-...
```

Never expose keys in browser clients; use a backend proxy for public apps.

---

## 6. Wallet & top-up

**Personal Center → Wallet**: Alipay, WeChat Pay, USDT, redemption codes — as shown at checkout. Credits share one balance with API usage.

---

## 7. Support

- **Primary — Telegram:** [@ZXCZCI](https://t.me/ZXCZCI) — onboarding, billing, group questions, USDT.  
- **Backup — email:** [yeallen441@gmail.com](mailto:yeallen441@gmail.com?subject=Vector%20Engine%20API%20support) — if Telegram is unavailable; never paste `sk-` keys.  
- **Docs only — GitHub Issues:** [Archer-ai-hub/vectorengine-api-gateway/issues](https://github.com/Archer-ai-hub/vectorengine-api-gateway/issues) — typos / links in this repo, not account disputes.  
- **Console:** tickets / support where available.

---

## Operator

**Chongqing Ruize Zhijie Technology Co., Ltd.** · 重庆瑞泽智界科技有限公司

---

*If this file conflicts with the live console or Apifox, trust the live sources.*
