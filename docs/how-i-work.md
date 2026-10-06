# How I Work

## What I take on

- Custom n8n workflows built to your requirements
- Adding AI steps (classification, extraction, scoring, summarization) to new or existing workflows
- Reviewing, fixing and hardening existing workflows: error handling, retries, deduplication, input validation
- Connecting n8n to tools you already use (Google Workspace, Telegram, Slack, CRMs, databases, webhooks)

## Process

1. **Requirements:** you describe the problem, the inputs and the result you want. I reply with scope, assumptions and open questions.
2. **Build:** I build with synthetic or sanitized data, never your production data.
3. **Test:** I write test cases for normal, edge, duplicate and failure scenarios and share the results.
4. **Handover:** you receive the workflow JSON, a README (setup, credentials, placeholders, known limits) and the test cases.

## Principles

- **AI never makes the final decision on its own.** Code validates AI output, and anything uncertain goes to a human review path.
- **Untrusted input stays data.** Emails, files and form fields are never treated as instructions.
- **Nothing is lost silently.** Failures are visible and records are saved before notifications go out.
- **You keep control of your accounts.** You create the credentials in your own n8n instance; I never need your passwords.

## What I need from you

- A description of the process today, with a few anonymized examples
- Which tools and accounts are involved
- What counts as success, and what must never happen automatically
- Your n8n setup (cloud or self-hosted, version if known)

## Data handling

I work with sample or anonymized data wherever possible. If real data passes through an AI provider, tell me up front so we can check the provider's data terms and decide what to mask.

## Contact

Via Upwork or Fiverr (links in the main README).
