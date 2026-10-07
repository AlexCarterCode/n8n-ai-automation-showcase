# n8n AI Automation Showcase

Practical n8n automation workflows focused on AI-assisted business processes, validation, routing, and human review.

## What I Build

I build n8n workflows that connect business inputs to structured decisions and actions.

The focus is not just adding AI to a workflow. Each automation includes validation, structured outputs, routing logic, error handling, and human review where appropriate.

## Showcases

### 01 — AI Lead Qualification & Routing

**Business problem**

Sales teams receive many incoming leads and need to quickly determine which opportunities deserve attention.

**Workflow**

`New Lead → Validate → Normalize → Duplicate Check → AI Qualification → Score → Route`

The workflow evaluates lead information and produces:

- Lead score
- Priority
- Confidence
- Qualification reasons
- Missing information
- Recommended action

It routes leads into outcomes such as `HOT`, `WARM`, `COLD`, or `NEEDS_REVIEW`.

**Highlights**

- Input validation and normalization
- Duplicate handling
- Structured AI output
- Confidence-based review
- Deterministic security checks
- Sales routing

[View Lead Qualification →](./showcase-upload/01-lead-qualification/)

---

### 02 — AI Invoice Extraction & Validation

**Business problem**

Invoice information often arrives in unstructured documents. Manually extracting and checking the data is repetitive and error-prone.

**Workflow**

`Invoice Input → Extract → Validate → Normalize → Deduplicate → Determine Status → Store / Review`

The workflow extracts structured invoice information and uses deterministic logic for validation and downstream decisions.

**Highlights**

- Structured invoice extraction
- Field validation
- Duplicate handling
- Due-date/status logic
- Human review for uncertain cases
- Structured storage

[View Invoice Extraction →](./showcase-upload/02-invoice-extraction/)

---

### 03 — AI Email Triage & Routing

**Business problem**

Shared business inboxes often contain sales requests, support issues, billing questions, internal messages, and irrelevant emails.

**Workflow**

`Email → Understand → Classify → Prioritize → Route`

The workflow classifies incoming emails and produces:

- Category
- Priority
- Confidence
- Reason
- Recommended action
- Review status

It routes messages to the appropriate queue and alerts humans when required.

**Highlights**

- Gmail/webhook/manual input handling
- Structured AI classification
- Priority routing
- Duplicate/thread handling
- Prompt-injection safeguards
- Retry and error handling
- Human review
- No automatic email replies

[View Email Triage →](./showcase-upload/03-email-triage/)

---

## Approach

My automation approach is:

```text
Input
  ↓
Validate
  ↓
Normalize
  ↓
AI / Rules
  ↓
Validate Decision
  ↓
Route
  ↓
Human Review when needed
```
AI is used where unstructured information needs interpretation.
Deterministic workflow logic is used where predictable validation, routing, deduplication, or business rules are more appropriate.
## Tech

- n8n
- AI / LLM APIs
- Webhooks
- Gmail
- Google Sheets
- Telegram
- JSON
- JavaScript

## Security & Data Handling

The public workflows use synthetic/example data and are prepared for public inspection.

Credentials and secret values are not included in the public workflow exports.

AI-assisted workflows treat external text as untrusted input and include validation/review boundaries where appropriate.

For real deployments, integrations and data-handling requirements should be reviewed against the customer's environment and provider policies.

## About

I build practical n8n automations for businesses that want to reduce repetitive manual work and connect AI with existing workflows.

If you need an n8n workflow built, debugged, or improved, feel free to reach out.
