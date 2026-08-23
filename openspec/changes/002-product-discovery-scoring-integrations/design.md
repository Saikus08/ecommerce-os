# Design Notes — Product Discovery, Scoring & Integration Spike

## Principle

No opaque “AI score”. Every score must be explainable, formula-driven, and backed by observed/calculated inputs. Human decisions remain `GateDecision`; the system provides evidence, calculations, warnings and recommendations.

## Data posture

- Data-intensive, not Big Data.
- PostgreSQL is the source of truth.
- Normalize fields needed for querying, calculations, scoring and decisions.
- Keep `raw_payload` JSONB for external responses, exports or structured manual captures.
- Snapshot data that changes over time.
- Distinguish `OBSERVED`, `CALCULATED`, and `INFERRED` where it materially affects trust.

## Demand Score — 0 to 100

Measured primarily with Nubimetrics/Mercado Libre evidence:

| Weight | Component |
|--------|-----------|
| 35% | Units sold/month |
| 25% | Search volume / purchase intent |
| 20% | Sales trend over 90/180 days |
| 20% | Stability vs seasonality |

Do not use only “sells 500 units/month”. Uruguay is small. The more useful concept is:

```text
accessible demand = monthly demand × reasonably capturable market share
```

Operational question:

> Can we sell a reasonable initial lot in <= 90 days capturing roughly 3–10% of the market?

Initial output should include:

- monthly observed/estimated demand;
- assumed capturable share;
- accessible monthly demand;
- 90-day accessible units;
- score component breakdown;
- uncertainty/source notes.

## Competition Score — 0 to 100

100 means attractive market.

| Weight | Component |
|--------|-----------|
| 30% | Sales per seller/listing: offer vs demand |
| 25% | Top 5 / Top 10 sales concentration |
| 20% | Mercado Líder / dominant seller concentration |
| 15% | Catalog sales participation |
| 10% | Price pressure / product homogeneity |

Examples:

- 1,000 sales/month + 8 relevant sellers may be interesting.
- 1,000 sales/month + 150 sellers + Top 3 controlling 80% is less attractive.

Initial output should include:

- relevant sellers/listings count;
- top seller/listing concentration;
- Mercado Líder/dominant seller share;
- catalog participation;
- price dispersion/homogeneity indicators;
- score component breakdown;
- uncertainty/source notes.

## Unit economics

Do not start with a unit economics score. Start with real financial numbers.

Per unit:

```text
sale price
- Mercado Libre commission
- Mercado Libre logistics/costs
- taxes/associated charges
- landed cost
- fulfillment/packaging
- returns/warranty allowance
- estimated CAC/ads
= contribution profit
```

Landed cost:

```text
product cost
+ freight China→Uruguay
+ insurance
+ import duties/taxes
+ customs broker
+ local transport
+ QC/packaging
```

Decision metrics:

- contribution profit/unit;
- contribution margin %;
- break-even ROAS;
- ROI on lot;
- capital required;
- months to recover inventory;
- sensitivity to price -10%, landed cost +15%, CAC +30%.

Scenarios:

- optimistic;
- base;
- stress.

## Opportunity Score — 0 to 100

Only after demand, competition and economics are calculated:

| Weight | Component |
|--------|-----------|
| 30% | Demand |
| 25% | Competition |
| 30% | Economics |
| 15% | Risk / Operational Fit |

Risk / Operational Fit includes:

- size/weight;
- fragility;
- regulation/certifications;
- returns;
- warranty;
- variant complexity;
- MOQ;
- required capital.

## Hard gates

Hard gates override aggregate score.

| Rule | Result |
|------|--------|
| Insufficient demand | NO-GO |
| Negative economics | NO-GO |
| Capital required > budget | NO-GO |
| Critical regulatory/logistics risk | NO-GO |
| Score >= 70 without hard fails | GO |
| Score 55–69 | REVIEW |
| Score < 55 | NO-GO |

The initial 70/55 thresholds are parameters and must be calibrated with real candidates.

## Integration strategy

## Initial public documentation findings

Sources checked in this spike start:

- Mercado Libre Developers Uruguay: `items-y-busquedas`.
- Mercado Libre Developers Uruguay: `dominios-y-categorias`.
- Mercado Libre Developers Uruguay: `comision-por-vender`.
- Nubimetrics public product page: `producto/mercado`.
- Nubimetrics `/api/` returned 404 at time of check.

### Mercado Libre initial findings

- Uruguay site appears as `MLU` with currency `UYU` in Mercado Libre site/category docs.
- Search/listing docs expose useful resources such as `/sites/$SITE_ID/search`, `/items?ids=...`, `/users?ids=...`, and seller item search resources.
- Public search/listing data must be treated carefully: `available_quantity` is documented as referential/ranged, not exact stock.
- Category/domain docs expose site categories, category details, category attributes and domain discovery.
- Cost docs confirm a read-only `listing_prices` calculator under `/sites/$SITE/listing_prices` with filters such as `price`, `category_id`, `currency_id`, `listing_type_id`, `logistic_type`, `shipping_mode`, `billable_weight`, and `quantity`.
- Cost docs warn that shipping/fixed fee accuracy depends on logistics parameters; this supports using the official calculator instead of hardcoded fee tables.
- The examples are mostly for other sites such as `MLA`; we still need to validate behavior for `MLU` specifically.

### Nubimetrics initial findings

- Public product page confirms relevant capabilities conceptually: products searched, products offered, products sold, category sales, searched keywords, units sold, seller rankings, monthly sales, growth, concentration and seasonality signals.
- Public site describes dashboard/product capabilities, not a confirmed public API.
- `https://nubimetrics.com/api/` returned 404 at time of check.
- Treat Nubimetrics as dashboard/manual/export until official API/export and contract permissions are verified.

### Mercado Libre

Research/validate before implementation:

- categories/domains for Uruguay site `MLU`;
- search/listings endpoints;
- item detail endpoints;
- seller endpoints;
- trends/reviews/questions where available;
- fee/cost calculator endpoint for site/category/listing type/logistics;
- authentication requirements;
- rate limits and terms.
- whether `listing_prices` works for `MLU` with the required logistics and category parameters.

Likely implementation shape after verification:

- concrete `MercadoLibre::Client`;
- importers/mappers for listings, sellers, search result snapshots and fee estimates;
- idempotent jobs for snapshot runs;
- synthetic fixtures in specs.

### Nubimetrics

Research/validate before implementation:

- official API availability;
- CSV/XLS export availability;
- dashboard/manual capture terms;
- metric definitions;
- contract permissions for storage/processing;
- update cadence;
- whether data is observed, estimated or inferred.

Likely implementation shape depends on result:

1. API client if official and allowed.
2. Export importer if CSV/XLS is available and allowed.
3. Structured manual capture if dashboard-only.
4. Evidence-only reference if storage/processing is not allowed.

Do not design ingestion around assumed Nubimetrics payloads.

## Candidate implementation slices after spike

1. Market research foundation: `MarketResearch`, `MarketSnapshot`, normalized manual/source metrics.
2. Demand and competition assessments with formulas and tests.
3. Economics scenarios with deterministic calculations and hard gates.
4. Opportunity assessment and GO/REVIEW/NO-GO recommendation.
5. Mercado Libre integration spike implementation with synthetic/public test data only.
6. Nubimetrics ingestion path depending on verified availability.
7. Sourcing readiness slice, not full sourcing execution.
