# Public safety checklist

Before committing this directory:

- No API keys, tokens, cookies, passwords, private keys, or OAuth secrets.
- No real customer/vendor/employee data.
- No real email addresses unless intentionally public and necessary.
- No production URLs, webhook URLs, spreadsheet IDs, chat IDs, database URLs, or infrastructure addresses.
- Only `.example` domains and fictional values in test data.
- Synthetic documents contain no real metadata-sensitive business data.
- Do not add n8n credential exports.
- Do not add `.env` files.
- Do not add execution logs or screenshots containing private values.
- Run a secret scan before the first public commit.
