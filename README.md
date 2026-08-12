# 🎨 Urban Sketching Weather Advisor — n8n workflow

An AI-powered weather advisor for plein-air sketching: every morning at 8:00 it fetches the hourly forecast for Kraków (Open-Meteo), asks Claude to find the best 2-hour window for watercolor sketching outdoors, and sends an email — either with a recommended spot or an honest "skip today".

The full story of how this workflow came to be — including the three traps I fell into along the way (`[object Object]`, empty content from a thinking-enabled model, and JSON wrapped in markdown fences) — is described on my blog (in Polish): **[programistka.com — link to the post]**.

## 📦 What's inside

| File | Contents |
|---|---|
| `urban-sketching-weather-advisor.json` | Ready-to-import workflow — 8 nodes: Schedule Trigger → HTTP Request → Code (transform) → Anthropic → Code (defensive parsing) → IF → 2× Send Email |

## ✅ What you need

- **n8n** — Cloud (free 14-day trial) or self-hosted Community Edition
- **Anthropic API key** — [console.anthropic.com](https://console.anthropic.com); the minimum $5 top-up lasts for weeks
- **SMTP for sending emails** — e.g. Gmail with an App Password ([myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords), requires 2FA)

Open-Meteo requires no key and no registration (for non-commercial use).

## 🚀 Import in three steps

1. **Import the workflow:** in n8n → menu → **Import from File** → pick the JSON file from this repo.
2. **Connect your own credentials:** the **Ask Claude** node will ask for an Anthropic key, and both **Send Email** nodes for SMTP details. Replace `you@example.com` with your address in the **From Email** and **To Email** fields.
3. **Click Publish** (top right corner) — without it, the workflow won't run on schedule. For a manual test, **Execute workflow** is enough.

## 🔧 Make it yours

- **Different city:** change `latitude` and `longitude` in the **Fetch Weather (Open-Meteo)** node, plus the city name in the **Transform Hourly Data** node and in the prompt (including the list of sketching spots!).
- **Different weather criteria:** the temperature, wind, and cloud-cover thresholds are spelled out in the prompt in the **Ask Claude** node — just reword them.
- **Different hour:** **Daily at 8:00** node → Trigger at Hour.

## 💸 Costs

One run per day is a single Claude Sonnet 4.6 call on a short prompt — pennies per month. Open-Meteo and Gmail delivery are free.

## ❓ Questions

Leave a comment under the blog post at [programistka.com](https://programistka.com) 💬
