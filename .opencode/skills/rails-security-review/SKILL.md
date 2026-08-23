---
name: rails-security-review
description: Review E-commerce OS Rails security around secrets, sessions, external APIs, source payloads, logs, jobs, webhooks, scraping risk, and sensitive business data.
compatibility: opencode
---

# Rails Security Review

Use for auth/session, external APIs, tokens, exports/imports, source payloads, CORS, dependency, logging, and sensitive-data changes.

## Critical Checks

- No secrets or real credentials in code, docs, fixtures, logs, or screenshots.
- No `.env` reads.
- External API tokens are accessed only through environment/configuration boundaries.
- Logs do not expose full raw payloads if they can contain sensitive data.
- Imports validate source shape and fail safely.
- Jobs are idempotent and do not duplicate external data on retry.
- Browser automation is not used for scraping without explicit approval.
- CORS/session settings are explicit if browser/client boundaries change.

## External Data Risk

- Distinguish public, authenticated, own-account, contract-only, export-only, manual, and unavailable data.
- Do not assume Nubimetrics API availability.
- Do not store provider data beyond allowed contract/use terms.
- Keep source URL/reference and observed time when facts can change.

## Tooling

When appropriate:

- `bin/brakeman --quiet --no-pager --exit-on-warn --exit-on-error`
- `bundle exec bundler-audit check --update`
- focused RSpec specs for security-sensitive behavior

Do not treat tool output as complete security coverage. Inspect the code path.
