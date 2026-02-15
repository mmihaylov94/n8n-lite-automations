# n8n Automation Workflows (Lite)

Ready-to-use automation templates for n8n. Set up in minutes — no coding required.

These workflows help you capture leads from forms, get notified when payments happen, and connect your favorite tools like Google Sheets and Slack.

---

## What’s Included

### Lead Intake Webhook
**Best for:** Capturing form submissions (landing pages, contact forms, Typeform, Tally, etc.)

- Saves leads to Google Sheets
- Validates email addresses
- Optional Slack notifications
- Avoids duplicate entries

**Start here** — this is the easiest workflow to set up.

---

### Stripe Payment Webhook
**Best for:** Reacting to Stripe payments (one-time or checkout)

- Securely receives payment events from Stripe
- Optional Slack notifications when payments complete
- Handles both payment intents and checkout sessions

---

## Getting Started

1. **Have n8n ready** — Sign in to your n8n account (n8n Cloud or self-hosted).
2. **Pick a workflow** — We recommend starting with Lead Intake.
3. **Import the files** — Use **Workflows** → **Import from File** and choose the `.json` file from the right folder.
4. **Follow the setup guide** — Each workflow has a matching guide (`.md` file) with step-by-step instructions.
5. **Connect your tools** — Add your Google, Slack, or Stripe credentials when prompted.
6. **Turn it on** — Click **Activate** and you’re done.

---

## Files and Folders

| Workflow | Folder | What to import |
|----------|--------|----------------|
| Lead Intake | `02-lead-intake-lite/` | `02_lead_intake_lite.json` |
| Stripe Payment | `01-stripe-webhook-lite/` | `01_stripe_webhook_lite.json` + `util_stripe_verify_signature.json` |

**Tip:** For Stripe, import the helper workflow (`util_stripe_verify_signature.json`) first, then the main workflow. The setup guide has the full order.

---

## Finding Your Webhook URL

After you activate a workflow, n8n gives it a webhook URL. You’ll need this to connect your forms or Stripe.

**How to find it:**
1. Open your workflow in n8n.
2. Click the **Webhook** node (usually the first node on the left).
3. Look for **Production URL** or **Test URL** in the node panel.
4. Your full URL will look like: `https://your-instance.app.n8n.cloud/webhook/leads` (Lead Intake) or `.../webhook/stripe/payment` (Stripe).

Use this URL in your form builder’s webhook field, or when setting up Stripe webhooks.

---

## License
MIT License
