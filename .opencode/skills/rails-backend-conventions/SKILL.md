---
name: rails-backend-conventions
description: Apply E-commerce OS Rails conventions for models, controllers, services, queries, jobs, importers, snapshots, financial calculations, and PostgreSQL-backed domain logic.
compatibility: opencode
---

# Rails Backend Conventions

Read first when relevant: `AGENTS.md`, `openspec/project.md`, active OpenSpec change, accepted ADRs, and code-quality context.

## Backend Shape

- Rails full-stack app in the repository root.
- PostgreSQL is the source of truth.
- React is integrated inside Rails; server decisions stay server-side.
- Modular monolith; no microservices.
- ActiveRecord first. Avoid repositories and generic integration frameworks unless a real complexity demands them.

## Layer Rules

- Controllers: request boundary, params, orchestration, response/rendering.
- Models: persistence, associations, validations, scopes, simple predicates, normalization callbacks.
- Services: use-case orchestration, transactions, writes, deterministic calculations, and external side effects when needed.
- Queries: complex reads, dashboards, score inputs, market/economics reports.
- Jobs: idempotent import/snapshot orchestration through Solid Queue when asynchronous work is justified.
- Importers/adapters: concrete per source (`MercadoLibre`, `Nubimetrics`), not a generic provider abstraction.

## E-commerce OS Rules

- Every feature must answer: what concrete e-commerce decision improves?
- Keep observed facts, calculated values, and inferred conclusions distinguishable.
- Store normalized fields for querying/calculation and `raw_payload` JSONB for traceability where data came from an external source or structured capture.
- Use snapshots for data that changes over time: listings, sellers, search results, market metrics, fees, and imported/exported source data.
- Money and scores must be deterministic and tested. Use decimal/numeric, never floats, for financial values.
- Do not create `AiAnalysis` or opaque AI scoring. Scores are formula-driven and explainable.
- Do not assume Nubimetrics has an API. Validate API/export/manual/dashboard options before ingestion design.
- Do not scrape without explicit approval.

## Verification

Use focused checks:

- `bundle exec rspec path/to/spec.rb`
- `bin/rubocop`
- `bin/brakeman --quiet --no-pager --exit-on-warn --exit-on-error`
- `bin/verify`

Report skipped checks as justified `N/A`, not silence.
