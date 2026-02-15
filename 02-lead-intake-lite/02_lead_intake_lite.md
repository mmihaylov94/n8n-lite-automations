# Lead Intake — Setup Guide

When someone submits a form (landing page, Typeform, Tally, etc.), this workflow saves their info to Google Sheets and can send a Slack notification. Perfect for capturing leads without any coding.

---

## Before You Start

You’ll need:

- **n8n** — Your n8n account, signed in
- **Google Sheets** — A spreadsheet where leads will be saved
- **Slack** (optional) — Only if you want to get notified in Slack when a new lead comes in

---

## Step 1: Set Up Your Google Sheet

1. Create a new Google Sheet, or use an existing one.
2. At the bottom, add a new sheet/tab (the tabs are along the bottom). Name it something like **Leads**.
3. In the first row, add these column headers **exactly** (copy-paste works best):

   | lead_key | email | name | phone | source | status | created_at | raw_json | last_seen_at |

4. Save the sheet. If you use a different Google account for n8n, share this sheet with that account (Share → add the email).

---

## Step 2: Add Your Credentials in n8n

1. In n8n, open the main menu (☰) and go to **Credentials**.
2. Click **Add credential** → **Google Sheets**.
3. Sign in with the same Google account you used for the sheet.
4. If you want Slack notifications: **Add credential** → **Slack** and connect your workspace.

---

## Step 3: Import and Configure the Workflow

1. In n8n, go to **Workflows** (main menu) and click **Import from File**.
2. Choose **02_lead_intake_lite.json** from the `02-lead-intake-lite/` folder.
3. The workflow will open. You’ll see several boxes (nodes) connected with lines.
4. **Configure the Google Sheets node** (it’s labeled **GS:leads_upsert**):
   - Click it to open the settings.
   - Select your Google Sheets credential.
   - Choose your spreadsheet and the sheet tab (e.g. Leads).
   - Click outside the node to save.
5. **If you’re using Slack** — Click the **SLACK:notify_lead** node, choose your Slack credential and the channel for notifications.
6. **If you’re NOT using Slack** — Right‑click the **SLACK:notify_lead** node and choose **Delete**. Then drag a line from the **GS:leads_upsert** node’s output (right side) to the **RS:respond_ok** node’s input (left side), and remove any old connections to the deleted node.
7. Click **Save** (top right), then **Activate** to turn the workflow on.

---

## Step 4: Get Your Webhook URL

1. Click the first node on the left (the **Webhook** node).
2. In the panel on the right, find **Production URL** or **Test URL**.
3. Copy that URL. It will look like:  
   `https://your-instance.app.n8n.cloud/webhook/leads`

Use this URL in your form builder’s webhook or submit URL field (Typeform, Tally, etc.).

---

## What Data Can You Send?

Your form should send data in this format. Most form builders can do this automatically.

| Field | Required? | Example |
|-------|-----------|---------|
| email | Yes | `lead@example.com` |
| name | No | `Jane Doe` |
| phone | No | `+1234567890` |
| source | No | `landing-page` (helps you track where the lead came from) |

---

## How to Test It

**Option A — Use Postman (free)**

1. Download [Postman](https://www.postman.com/downloads/) (free).
2. Create a new **POST** request.
3. Enter your webhook URL in the address bar.
4. Go to **Body** → select **raw** → choose **JSON**.
5. Paste: `{"email":"test@example.com","name":"Test User","phone":"+1234567890","source":"manual-test"}`
6. Click **Send**. You should see a new row in your Google Sheet, and a Slack message if you configured it.

**Option B — Use your form builder**

Point your form’s webhook URL to the URL from Step 4 and submit a test response.

---

## Troubleshooting

- **Nothing appears in Sheets** — Check that the column headers in your sheet match exactly (including spelling and underscores).
- **"Invalid credentials"** — Make sure your Google Sheets credential is connected and the sheet is shared with that account.
- **Webhook returns an error** — The `email` field is required and must be a valid email format.
