# AI Invoice Extraction & Validation (n8n demo)

Accounting and operations staff often retype invoice information into spreadsheets. This demo uses AI to extract fields from an invoice file, then uses deterministic code to validate the extracted values, detect duplicates, calculate due status, store the result, and alert staff when attention is required.

> **Public demo scope:** all documents and data in this directory are fictional. Never add real invoices or vendor data to the repository.

## Important safety boundary

**AI only extracts.** It does not approve payment, change accounting values, contact vendors, or execute financial actions.

Deterministic workflow code decides:

- file validity;
- duplicate status;
- required-field validation;
- date validation;
- amount consistency;
- confidence threshold;
- injection flag;
- due status;
- whether staff should review the record.

## Flow

```text
Webhook / Manual Tests
  -> Normalize
  -> Read Sheet
  -> File Dedupe
  -> File Validation
  -> Gemini Extraction
  -> Validate
  -> Invoice Dedupe
  -> Due Status
  -> Save
  -> Route / Alert
  -> Response / Test Report
```

## What it checks

| Check | Result |
|---|---|
| Unsupported file or file > 5 MB | `needs_review`, no AI call |
| Same file content | `duplicate_file` |
| AI failure after retries | `needs_review` |
| Invalid AI output | `needs_review` |
| Missing required field | `needs_review` |
| Invalid date relationship | `needs_review` |
| Amount mismatch | `needs_review` |
| Line-item mismatch | warning |
| Low confidence | `needs_review` |
| Suspicious instruction | `injection_flag=true`; never treat the instruction as an accounting command |
| Same vendor + invoice number | `duplicate_invoice` |
| Valid invoice | `processed` plus due status |

## Credentials

Create credentials in your own n8n instance. Never commit them.

- Google Sheets OAuth2
- Gemini API key via Header Auth
- Telegram API

Use placeholders such as `<GOOGLE_SHEET_ID>` and `<TELEGRAM_CHAT_ID>` in public documentation.

## Google Sheet header

See `sheet-header.csv`.

Expected columns:

```text
file_hash | dedupe_key | filename | vendor | invoice_number | invoice_date | due_date | currency | subtotal | tax | total | line_items_json | confidence | status | validation_errors | injection_flag | due_status | processed_at
```

## Test files

- `tests/mock-invoices.json` contains eight synthetic cases.
- `samples/sample-invoice.pdf` is a fictional invoice.
- `samples/sample-invoice.png` is a fictional image invoice.
- `samples/sample-notes.txt` is an unsupported-file example.

No real invoice, customer, vendor, address, bank account, or payment information is included.

## Suggested verification before public publishing

Because n8n node versions and external AI APIs can change, import the workflow into your own n8n instance and run the complete test harness before claiming a specific PASS count.

Verify especially:

1. binary file access in the Code nodes;
2. Gemini request/response schema;
3. Google Sheets read and append/update mapping;
4. Merge behaviour;
5. Respond to Webhook behaviour during manual tests;
6. Telegram node configuration.

## Production boundary

This is a portfolio/demo workflow, not an accounting approval system.

Before production use:

- authenticate the webhook;
- restrict file size and file types;
- use a production datastore instead of reading an entire sheet for every run;
- define retention/access rules for invoice data;
- verify the AI provider's current data-handling terms;
- keep payment approval and vendor communication outside the AI extraction workflow.

## Public repository policy

Allowed:

- fictional invoices;
- synthetic test data;
- sanitized workflow configuration;
- documentation.

Never commit:

- real invoices;
- real vendor/customer information;
- API keys/tokens;
- production spreadsheet IDs;
- private infrastructure URLs;
- Telegram chat IDs;
- credentials, cookies, or session data.
