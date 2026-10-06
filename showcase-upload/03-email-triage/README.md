# AI Email Triage & Routing (n8n demo)

A shared B2B inbox can receive sales inquiries, support incidents, billing questions, internal messages, and irrelevant mail. This workflow understands, classifies, prioritizes, and routes each message so staff can focus on the right queue first.

**It never replies to anyone.** There is no send/reply email node in the demo. Humans handle every email.

## Flow

```text
Gmail Trigger / Webhook / Mock Tests
  -> Config
  -> Normalize
  -> Read Sheet
  -> Dedupe
  -> Pre-check
  -> AI Classification
  -> Validate & Decide
  -> Assign Queue
  -> Save to Sheet
  -> Route
  -> Optional Telegram Alert
```

## Categories

| Category | Queue | Alert |
|---|---|---|
| SALES | `sales` | HIGH / URGENT |
| SUPPORT | `support` | URGENT |
| BILLING | `billing` | none |
| INTERNAL | `internal` | none |
| OTHER | `other` | none |
| `needs_review` | `review` | none |

## Security behaviour

- Incoming email content is untrusted data.
- The AI prompt explicitly says not to follow instructions embedded in email text.
- The workflow uses strict output validation.
- `needs_review` is decided by workflow code, not by the model.
- Low confidence and AI failures go to manual review.
- Duplicate `email_id` values are stopped before AI processing.
- The record is saved before an alert is attempted.
- Telegram alert failure does not delete the saved record.
- Webhooks must be authenticated before public exposure.

## Injection test

Case 6 contains a real sales question plus text attempting to force an `URGENT` classification. The expected result is:

- category: `SALES`;
- `injection_flag=true`;
- priority must not be `URGENT`.

The workflow currently records the injection flag from both heuristic and AI signals. **Before production use, verify that an injection flag cannot cause an unwanted alert under your chosen alert policy.**

## Gmail

The shipped workflow keeps the Gmail Trigger disabled for demo safety. There is no email send/reply node.

Do not describe the Gmail OAuth credential as a security guarantee of "read-only" access. The important application-level boundary is that this workflow contains no send/reply node and does not automatically respond to customers.

## Google Sheet header

See `sheet-header.csv`.

```text
email_id | thread_id | sender | subject | category | priority | confidence | reason | recommended_action | status | queue | label | injection_flag | processed_at
```

## Test cases

`tests/mock-emails.json` mirrors the eight synthetic cases used by the workflow:

1. Sales inquiry
2. Production outage
3. Invoice error
4. Internal reminder
5. Too-vague request
6. Prompt injection + real pricing question
7. Simulated AI failure
8. Duplicate of case 1

The workflow's own test harness is the authoritative test input because it is embedded in the imported JSON. The external JSON file is a public reference copy.

## Credentials

Create your own credentials in n8n:

- Google Sheets OAuth2
- Gmail OAuth2 (real inbox mode only)
- Gemini API key through Header Auth
- Telegram API

Never commit credentials, API keys, chat IDs, spreadsheet IDs, cookies, or production URLs.

## Public test procedure

1. Create a synthetic Google Sheet using `sheet-header.csv`.
2. Import `email-triage-workflow.json`.
3. Attach your own credentials and replace placeholders inside n8n.
4. Keep Gmail Trigger disabled.
5. Run the built-in `Run Test Cases`.
6. Inspect `Test Report`.
7. Verify duplicate behaviour.
8. Only after verification, consider enabling real Gmail input.

## Known demo limits

- The entire sheet is read for dedupe, which is suitable for a demo but not high-volume production.
- AI/API behaviour can change with provider/model versions.
- Alert volume depends on the AI's validated priority for SALES messages; do not hard-code a claim such as "exactly one Telegram alert" unless your actual run proves it.
- Attachments, thread summarization, auto-reply, and dashboards are intentionally out of scope.

## Data handling

If real email data is used, the email content is sent to the configured AI provider and stored in the configured Google Sheet. Review the current provider terms, access controls, retention, and organizational data policy before using customer mail.

## Public repository policy

This directory contains only sanitized configuration, synthetic email examples, and documentation. Replace all private placeholders inside n8n, not inside this repository.
