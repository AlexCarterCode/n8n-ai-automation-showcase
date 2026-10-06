# n8n AI Automation Showcase

Three production-style n8n workflows that put AI to work on everyday business tasks: qualifying leads, extracting invoice data, and triaging a shared inbox.

The design rule behind all three: **AI understands, code decides.** The model reads and extracts; plain code validates, scores, deduplicates and routes. Untrusted input (leads, invoices, emails) is treated as data, never as instructions.

## Demos

| # | Workflow | What it does | Stack |
|---|---|---|---|
| 1 | [AI Lead Qualification & Routing](01-lead-qualification/) | Validates and normalizes inbound leads, scores them (rules + AI), routes HOT / WARM / COLD / NEEDS_REVIEW | Webhook, Gemini, Code |
| 2 | [AI Invoice Extraction & Validation](02-invoice-extraction/) | Extracts fields from PDF/PNG/JPG invoices, validates amounts and dates, dedupes, stores in Google Sheets, alerts on Telegram | Webhook, Gemini, Google Sheets, Telegram |
| 3 | [AI Email Triage & Routing](03-email-triage/) | Classifies and prioritizes incoming email, routes it to the right queue, alerts staff on urgent items. Never replies to anyone | Gmail, Gemini, Google Sheets, Telegram |

## What these demos show

- **Reliable AI output:** structured JSON schemas, strict validation, retries, and a `NEEDS_REVIEW` path whenever the model fails or is unsure.
- **Prompt-injection awareness:** input is wrapped as untrusted data, suspicious instructions are flagged, and final decisions are made by code.
- **Idempotency:** duplicates are detected (file hash, vendor + invoice number, email ID, lead email) before any paid AI call.
- **Safe failure:** records are saved before alerts are sent, and a failed alert never loses data.
- **Built-in tests:** every demo comes with synthetic test data covering normal, edge-case, duplicate, injection and failure scenarios.

## Quick start

1. Pick a demo folder and read its README.
2. Import the workflow JSON into n8n.
3. Create your own credentials (Gemini API key as Header Auth, Google Sheets, Telegram) and fill the placeholders.
4. Run the test cases and compare against the expected results in the README.

No credentials, production URLs or real data are included in this repository. All sample data is synthetic.

## Work with me

I build custom n8n workflows and AI integrations to your requirements: new automations, AI steps added to existing flows, fixing or hardening workflows that already exist.

