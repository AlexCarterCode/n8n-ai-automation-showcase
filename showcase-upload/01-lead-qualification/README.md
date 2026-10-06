# AI Lead Qualification & Routing (n8n)

A B2B sales team receives more leads than it can review consistently. This workflow validates and normalizes an incoming lead, checks for duplicates, combines deterministic rules with AI analysis, assigns a qualification result, and routes the lead to the appropriate next step.

> **Public demo scope:** synthetic data only. No credentials, production IDs, private URLs, or real customer data belong in this directory.

## Business problem

Sales teams often spend time manually reading and prioritizing inbound leads. That can cause:

- good leads to wait too long;
- inconsistent qualification;
- sales time spent on poor-fit requests;
- weak auditability when a lead is routed incorrectly.

## Flow

```text
Webhook
  -> Validate & Normalize
  -> Duplicate Check
  -> Rules + AI Score
  -> Hard Rules / Decision
  -> Route
  -> Store
  -> Response
```

## What it demonstrates

| Step | Behaviour |
|---|---|
| Validate & Normalize | Cleans and validates the incoming lead without inventing missing information. |
| Duplicate Check | Detects a previously processed email and prevents another qualification run. |
| Hybrid scoring | Combines deterministic business rules with an AI fit score. |
| Hard rules | Business rules remain authoritative for the final qualification. |
| Manual review | Low confidence, contradictory data, AI failure, or security concerns should not become an automatic HOT decision. |
| Route | HOT, WARM, COLD, and NEEDS_REVIEW go to different next steps. |
| Store + Response | Returns/logs the qualification result and audit fields. |

## Input

Typical fields:

```json
{
  "name": "Linh Tran",
  "email": "linh@brightpath-agency.example",
  "company": "BrightPath Agency",
  "company_size": "25 employees",
  "need": "Automate lead follow-up and weekly sales reporting",
  "budget": "$6k",
  "timeline": "this month"
}
```

All example domains use `.example`.

## Output

A qualification result should include the workflow's score/priority, reasons, confidence, route, and audit timestamps. The exact fields are defined by the imported workflow JSON.

## Test data

`tests/sample-leads.json` contains six synthetic cases covering:

1. HOT
2. WARM
3. COLD
4. contradictory data
5. prompt-injection text
6. invalid input

The test data is documentation/demo data and is not a credential or production dataset.

## Setup

1. Import `lead-qualification-workflow.json` into n8n.
2. Create your own Gemini API credential and attach it to the AI node.
3. Replace any workflow placeholders with your own private values inside n8n.
4. Protect the public webhook with authentication before exposing it.
5. Run the supplied synthetic tests.
6. Verify duplicate behaviour by sending the same synthetic lead twice.

Do **not** put your Gemini API key, webhook URL, Google Sheet ID, production CRM ID, or other private values into this repository.

## Security notes

- Incoming lead fields are untrusted input.
- Never let model output override deterministic business rules.
- Prompt-injection text must be treated as data, not instructions.
- Before calling this workflow production-ready, verify that the current workflow JSON explicitly routes suspicious/injection cases to `NEEDS_REVIEW` rather than relying only on the model's classification.
- Do not use real customer leads in the repository's test files.
- If a real secret is ever committed, revoke/rotate it immediately and remove it from Git history before making the repository public.

## Known demo limits

- Storage is intended for a small demo unless replaced with a production datastore.
- Duplicate detection means a repeated test email may be skipped.
- AI output depends on the configured model/API.
- Test expectations should be checked against the actual imported workflow before publishing claims such as "all tests pass."

## Public repository policy

This directory intentionally contains:

- sanitized workflow configuration;
- synthetic `.example` data;
- documentation;
- reproducible test inputs.

It must not contain:

- API keys or tokens;
- real customer data;
- private infrastructure URLs;
- real spreadsheet/document IDs;
- credentials or cookies;
- production webhook URLs.
