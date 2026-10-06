# Showcase upload package

This package contains the public-safe supporting files for the three n8n demos.

Add the three existing workflow exports yourself:

- `01-lead-qualification/lead-qualification-workflow.json`
- `02-invoice-extraction/invoice-extraction-workflow.json`
- `03-email-triage/email-triage-workflow.json`

Do not replace those JSON files with raw credential exports or production copies.

Before public commit, run a secret scan and inspect the Raw view of every JSON.
