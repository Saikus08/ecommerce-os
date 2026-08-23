---
name: product-change-evaluation
description: Independently evaluate E-commerce OS changes against OpenSpec, business decision impact, evidence, tests, integration gates, financial correctness, and architectural drift.
compatibility: opencode
---

# Product Change Evaluation

Use for read-only evaluation of a diff or completed slice.

## Inputs

- `AGENTS.md`
- `openspec/project.md`
- active OpenSpec change/tasks/design
- accepted ADRs
- diff
- test/check evidence

## Evaluation Steps

1. Confirm scope and e-commerce decision improved.
2. Map requirements to implementation.
3. Map implementation to evidence.
4. Identify behavior not authorized by the spec.
5. Inspect material risk: migrations, financial calculations, external integrations, imports/jobs, raw payloads, security, architecture.
6. Check that scores/calculations are deterministic and explainable.
7. Classify findings as blocker or residual.
8. Return `pass`, `conditional pass`, or `fail`.

## Output

Use at most six sections:

- State/scope.
- Findings.
- Evidence and justified `N/A`.
- Drift.
- Blockers.
- Gates/next step.

Do not edit files. Do not accept the implementer summary as sole evidence.
