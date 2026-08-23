---
name: rails-database-patterns
description: Design E-commerce OS Rails/PostgreSQL migrations, constraints, indexes, JSONB raw payloads, snapshots, idempotent imports, and financial schema safely.
compatibility: opencode
---

# Rails Database Patterns

Use for migrations, schema design, query objects, indexes, constraints, snapshots, imports, market metrics, and financial calculations.

## Migration Rules

- Prefer reversible `change` migrations when possible.
- Use `up`/`down` when reversibility is not automatic.
- Avoid destructive changes without a material gate.
- Do not edit migrations that have already been shared or run beyond local-only scope.
- Add foreign keys, `null: false`, unique constraints, and check constraints when they express real invariants.
- Index foreign keys and common lookup predicates.

## Data-Intensive Rules

- PostgreSQL first; no Big Data tooling until a concrete bottleneck exists.
- Normalize fields needed for search, filters, calculations, scoring, and decisions.
- Keep `raw_payload` JSONB for external API responses, exports, or structured manual source captures where traceability matters.
- Use temporal snapshots for mutable external facts.
- Add idempotency keys/unique indexes for imports and snapshot runs.
- Postpone GIN indexes on JSONB until a real query requires them.

## Financial And Score Data

- Money: `decimal`, explicit precision/scale, currency field where needed.
- Percentages/rates: `decimal`, not float.
- Scores: integer 0..100 or decimal only if precision is required; add check constraints.
- Store formula inputs and outputs separately enough to explain a decision.
- Do not let aggregate opportunity score hide hard-gate failures.

## Performance Review

Check:

- WHERE/JOIN columns indexed.
- Composite index order: equality predicates first, then ranges/order.
- Snapshot lookup patterns by candidate/source/observed_at.
- No long transactions around external API work.
- No external HTTP calls inside DB transactions.

## Migration Evidence

For local reversible work, prefer:

- `bin/rails db:migrate`
- `bin/rails db:rollback STEP=1` when safe and relevant
- `bin/rails db:migrate`
- focused specs
