---
name: spec-driven-implementation
description: Implement approved E-commerce OS OpenSpec changes through small Rails/React slices with gates, evidence, and drift tracking.
compatibility: opencode
---

# Spec Driven Implementation

Use when implementing product behavior from `openspec/changes/` or accepted specs.

## Preconditions

Read:

- `AGENTS.md`
- `openspec/project.md`
- active `openspec/changes/<change>/proposal.md`, `design.md`, `tasks.md`
- relevant ADRs in `docs/adr/`
- `.opencode/context/project/project-context.md`
- `.opencode/context/core/code-quality.md`

Stop if the change is draft, approval is missing for material work, acceptance is unclear, or the task requires unapproved secrets, real data, external mutation, scraping, cloud, deployment, or destructive migration.

## Workflow

1. State the concrete e-commerce decision improved.
2. Pick the smallest vertical slice.
3. Map requirement -> test -> implementation -> verification.
4. Write tests first when behavior changes.
5. Keep changes inside approved scope.
6. Run proportional checks.
7. Report evidence, justified `N/A`, drift, risk, and gates.

## Material Gates

Human approval is required before push, deploy, cloud, real data/secrets, destructive migrations, external systems, new unplanned dependencies, release, or material architecture/security/privacy/business decisions.

Mandatory independent evaluation for migrations, financial calculations, imports/jobs, integrations, security, concurrency, or architecture changes.
