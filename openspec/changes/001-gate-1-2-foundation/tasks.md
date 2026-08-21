# Tasks — Gate 1–2 Foundation

## 1. Architecture decisions

- [x] Decide Rails full-stack + React integrated.
- [x] Decide normalized data + raw JSONB payload.
- [x] Decide external entities + temporal snapshots.
- [x] Decide simple seller model for market structure.
- [x] Decide generic GateDecision for future gates.
- [x] Decide not to implement AI analysis yet.

## 2. Research before implementation

- [x] Investigate Mercado Libre official capabilities for Gate 1–2.
- [x] Investigate Nubimetrics integration/export/API options.
- [ ] Decide supported acquisition methods for v1.
- [x] Define documented PASS/HOLD/REJECT rubric for Gate 1.
- [x] Define documented PASS/HOLD/REJECT rubric for Gate 2.

## 3. Rails scaffolding

- [x] Confirm Ruby/Rails/Node direction: modern Rails 8+, Ruby latest available, Node 24+ if compatible.
- [x] Get explicit OK for first `rails new`.
- [x] Generate Rails app with PostgreSQL and React integration.
- [x] Add minimal local verification command.
- [ ] Configure local PostgreSQL credentials/access for `db:prepare` without committing secrets.

## 4. Domain implementation — later

- [ ] Specify ProductCandidate requirements.
- [ ] Specify GateDecision requirements.
- [ ] Specify EvidenceItem/provenance requirements.
- [ ] Specify MarketResearch requirements.
- [ ] Specify snapshot/import idempotency requirements.
