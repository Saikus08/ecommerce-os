# Tasks — Product Discovery, Scoring & Integration Spike

## 1. Scope and architecture

- [x] Expand product scope in harness to include discovery → demand → competition → economics → score/risk → GO/REVIEW/NO-GO → sourcing/test/scale.
- [ ] Decide whether this spike updates `openspec/project.md`, creates ADRs, or remains an OpenSpec change until approved.
- [ ] Define final domain boundaries and names for ProductCandidate → MarketSnapshot → EconomicsScenario → Decision.
- [ ] Decide which gates are product-inminent vs still conceptual.

## 2. Scoring model

- [ ] Specify Demand Score formula with input definitions, normalization and missing-data behavior.
- [ ] Specify Competition Score formula with input definitions, normalization and missing-data behavior.
- [ ] Specify EconomicsScenario calculations with optimistic/base/stress examples.
- [ ] Specify Opportunity Score formula and hard gates.
- [ ] Define calibration parameters and where they live.

## 3. Data model spike

- [ ] Identify normalized fields for market snapshots.
- [ ] Identify normalized fields for demand/competition assessments.
- [ ] Identify normalized fields for unit economics scenarios.
- [ ] Decide what needs `raw_payload` and what is purely calculated.
- [ ] Define idempotency requirements for imports/snapshots.

## 4. Mercado Libre verification

- [ ] Verify public vs authenticated endpoints for Uruguay `MLU` categories/search/items/sellers.
- [x] Confirm public docs for site/categories/search/items/sellers exist.
- [x] Confirm public docs for fee/cost calculator endpoint exist.
- [ ] Verify fee/cost calculator behavior for `MLU` and required inputs.
- [ ] Verify availability of trends/reviews/questions for Gate 2 evidence.
- [ ] Document rate limits, auth, terms and integration risks.
- [ ] Decide v1 Mercado Libre acquisition methods.

## 5. Nubimetrics verification

- [ ] Verify whether an official API exists for required metrics.
- [x] Confirm public product page advertises relevant demand/competition metrics.
- [x] Confirm `/api/` is not a public documentation endpoint at time of check.
- [ ] Verify export availability and format if API is unavailable.
- [ ] Verify dashboard/manual capture feasibility and contract limits.
- [ ] Document metric definitions and whether values are observed, estimated or inferred.
- [ ] Decide v1 Nubimetrics acquisition methods.

## 6. Resulting implementation plan

- [ ] Break approved implementation into small slices.
- [ ] Define verification requirements per slice.
- [ ] Identify which slices need independent product/security/database evaluation.
