# Stripe Payment Webhook — Setup Guide

This workflow lets n8n receive payment events from Stripe (e.g. when a payment succeeds or a checkout completes) and optionally send a Slack notification. It’s secure and verifies that events really come from Stripe.

---

## Before You Start

You’ll need:

- **n8n** — Your n8n account, signed in
- **Stripe** — A Stripe account (use Test mode for testing)
- **Slack** (optional) — Only if you want payment notifications in Slack

---

## Step 1: Create a Place to Store Your Stripe Secret

n8n needs a safe place to store your Stripe webhook secret. We use a Data Table for this.

1. In n8n, open the main menu (☰) and go to **Data Tables**.
2. Click **Create Data table**.
3. Name it: `variables`
4. Add two columns: **key** (Text) and **value** (Text).
5. Create the table.

---

## Step 2: Import the Helper Workflow First

This workflow uses a small helper to check that requests are really from Stripe.

1. In n8n, go to **Workflows** and click **Import from File**.
2. Import **util_stripe_verify_signature.json** from the `01-stripe-webhook-lite/` folder.
3. Open that workflow. Click the **Data Table** node (or the node that reads from a table).
4. Point it to your `variables` table (the one you created in Step 1). You’ll add the Stripe secret to this table in Step 4.
5. Save the workflow.

---

## Step 3: Import and Configure the Main Workflow

1. Import **01_stripe_webhook_lite.json** from the `01-stripe-webhook-lite/` folder.
2. Click the **XW:util_stripe_verify_signature** node. In the dropdown, select **util_stripe_verify_signature** (the helper workflow you imported in Step 2).
3. **If you’re using Slack** — Click **SLACK:notify_payment**, choose your Slack credential and the channel for notifications.
4. **If you’re NOT using Slack** — Right‑click **SLACK:notify_payment** and choose **Delete**. Then connect the **IF:event_type_supported** node directly to **RS:respond_ok**: drag a line from the output of IF:event_type_supported to the input of RS:respond_ok, and remove any old connections.
5. Save the workflow and click **Activate**.

---

## Step 4: Connect Stripe to Your Webhook

1. In your workflow, click the **Webhook** node (first node on the left).
2. Copy the **Production URL** or **Test URL** (e.g. `https://your-instance.app.n8n.cloud/webhook/stripe/payment`).
3. Open the [Stripe Dashboard](https://dashboard.stripe.com) → **Developers** → **Webhooks**.
4. Click **Add endpoint**.
5. Paste your webhook URL into the **Endpoint URL** field.
6. Select these events: **payment_intent.succeeded** and **checkout.session.completed**.
7. Click **Add endpoint**.
8. On the new endpoint page, click **Reveal** under **Signing secret** and copy the value (it starts with `whsec_`).
9. Back in n8n, open your **variables** Data Table and add a row:
   - **key:** `stripe_secret`
   - **value:** paste the secret you copied

---

## How to Test It

**Option A — Stripe Dashboard (no extra tools)**

1. In Stripe Dashboard → **Developers** → **Webhooks** → click your endpoint.
2. Click **Send test webhook**.
3. Choose **payment_intent.succeeded** (or **checkout.session.completed**).
4. Click **Send test webhook**.
5. Check your Slack channel (if configured) and n8n’s execution history to confirm it ran.

**Option B — Stripe CLI (for advanced users)**

If you have the [Stripe CLI](https://stripe.com/docs/stripe-cli) installed:

```bash
stripe listen --forward-to https://YOUR-N8N-URL/webhook/stripe/payment
stripe trigger payment_intent.succeeded
```

---

## Troubleshooting

- **"Authenticated" or signature errors** — Make sure `stripe_secret` in your variables table matches the signing secret from Stripe, and that the webhook URL in Stripe matches your n8n webhook URL exactly.
- **No events in Slack** — Check that the Slack node has the correct credential and channel, and that the workflow ran (check Executions in n8n).
- **Events ignored** — This workflow only handles `payment_intent.succeeded` and `checkout.session.completed`. Other events will return “ignored” (that’s expected).
