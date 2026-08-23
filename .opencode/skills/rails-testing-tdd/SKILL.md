---
name: rails-testing-tdd
description: Write E-commerce OS RSpec tests for Rails models, services, importers, jobs, calculations, requests, and React-facing behavior with Red-Green-Refactor.
compatibility: opencode
---

# Rails Testing TDD

Use for backend behavior changes, new specs, test repair, and verification planning.

## Test Selection

- Model specs: validations, associations, scopes, normalization, constraints reflected at app level.
- Service specs: use-cases, transactions, deterministic scoring/economics calculations.
- Importer specs: mapping source payloads/exports to normalized models with synthetic fixtures.
- Job specs: import/snapshot orchestration, retries, idempotency.
- Request specs: server-rendered or JSON endpoints, validation and error states.
- System/component/frontend tests when UI behavior is material and tooling exists.

## Red -> Green -> Refactor

1. Write the smallest failing spec for the desired behavior.
2. Run the focused spec and confirm the failure proves the missing behavior.
3. Implement the smallest code change.
4. Run the focused spec until green.
5. Refactor in small steps while keeping specs green.
6. Run related specs and broader checks when proportional.

## Spec Standards

- Use synthetic data only unless real data has explicit approval.
- Prefer named subjects and minimal setup.
- Test formula examples with known numeric outputs.
- Test hard gates independently from aggregate score.
- Test idempotency for jobs/imports.
- Test invalid source payloads/exports without assuming perfect providers.

## Anti-Patterns

- Changing production behavior without a failing spec.
- Fixtures with real customer/supplier/market data.
- Testing only happy paths for financial decisions.
- Stubbing away the calculation being tested.
