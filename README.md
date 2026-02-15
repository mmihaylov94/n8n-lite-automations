# n8n Automation Workflows (Lite)

Production-ready n8n workflow templates built with clean structure and practical patterns — simplified for quick setup and testing.

This public repository contains **Lite versions** of two automation workflows designed to demonstrate secure webhook handling, validation logic, and structured business integrations without framework complexity.

---

## 📦 Included Workflows

### 1. Stripe Payment Webhook (Lite)

A secure Stripe webhook example.

**Features**
- Verifies Stripe webhook signatures  
- Handles `payment_intent.succeeded`  
- Handles `checkout.session.completed`  
- Returns structured JSON responses  
- Optional Slack notification  

Designed as a minimal, secure starting point for payment automation.

**Files**
- `01_stripe_webhook_lite.json`
- `01_stripe_webhook_lite.md`

---

### 2. Lead Intake Webhook (Lite)

A structured lead capture automation.

**Features**
- Webhook endpoint for form submissions  
- Email validation  
- Dedupe via `lead_key`  
- Google Sheets append/update  
- Optional Slack notification  
- Clean JSON responses  

Designed for quick deployment with form builders or landing pages.

**Files**
- `02_lead_intake_lite.json`
- `02_lead_intake_lite.md`

---

## What These Lite Workflows Demonstrate

- Clean branching logic  
- Secure webhook handling  
- Structured data normalization  
- Deterministic error responses  
- Practical third-party integrations  

They are intentionally lightweight and do not include advanced production features.

---

## What’s Not Included

These Lite versions do **not** include:

- Idempotency data tables  
- Structured run logging  
- Metrics tracking  
- Retry frameworks  
- Advanced observability patterns  
- AI-based automations  

Those features are part of the full Production Automation Framework.

---

## Getting Started

1. Run n8n (self-hosted or n8n Cloud).
2. Import one of the `.json` files into n8n.
3. Follow the corresponding `.md` setup guide.
4. Configure credentials.
5. Activate and test.

Each workflow includes detailed setup instructions.

---

## Intended Use

These workflows are suitable for:

- Learning structured automation patterns  
- Quick client demos  
- Testing webhook-based integrations  
- Lightweight internal automation  

For production deployments with structured logging, idempotency handling, and scalable architecture patterns, see the Pro version.

---

## 📄 License
MIT License

Copyright (c) [YEAR] [YOUR NAME]

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
