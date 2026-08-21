# Design Notes — Gate 1–2 Foundation

## Local configuration

- Local environment variables are loaded through `dotenv-rails` in development/test.
- `.env` is ignored and must not be committed.
- `.env.example` documents expected variables.
- For local PostgreSQL, use explicit variables: `POSTGRES_HOST`, `POSTGRES_PORT`, `POSTGRES_USER`, `POSTGRES_PASSWORD`.
- Reserve `DATABASE_URL` for platforms/environments that provide it explicitly, such as Railway/production.
- Do not use broad configuration shortcuts that obscure development/test behavior.

## Mercado Libre capability research — initial findings

Sources consulted:

- https://developers.mercadolibre.com.uy/es_ar/items-y-busquedas
- https://developers.mercadolibre.com.uy/es_ar/dominios-y-categorias
- https://developers.mercadolibre.com.uy/es_ar/opiniones-sobre-producto
- https://developers.mercadolibre.com.uy/es_ar/preguntas-y-respuestas
- https://developers.mercadolibre.com.uy/es_ar/tendencias

### Relevant for Gate 1–2

- Site/category data: `/sites`, `/sites/{site_id}/categories`, `/categories/{category_id}`, category attributes and domain discovery.
- Uruguay site is `MLU`, currency `UYU`.
- Search/listings: `/sites/{site_id}/search` supports active marketplace listings, relevance order, filters and sort options.
- Item detail/multiget: `/items?ids=...` supports fetching listing details and selected attributes.
- Seller lookup/multiget: `/users?ids=...` exposes seller data/reputation fields useful for market structure.
- Trends: `/trends/{site_id}` and `/trends/{site_id}/{category_id}` returns weekly trending keywords; useful for discovery but not sufficient alone for demand validation.
- Reviews: `/reviews/item/{item_id}` returns product reviews, rating average and rating levels where available.
- Questions: `/questions/search?item_id=...` returns questions for an item; useful for customer pain points where accessible.

### Caveats

- Some calls shown with `Authorization: Bearer`; we need to test which Gate 1–2 endpoints work publicly vs authenticated.
- `available_quantity` from public item/search resources is referential/ranged, not exact stock.
- Search relevance/ranking must be treated as a snapshot, not a permanent listing attribute.
- Trends are weekly keyword signals, not unit sales.
- Reviews/questions availability may depend on item/category/auth and should be treated as optional evidence.
- Do not assume Mercado Libre exposes competitor unit sales, GMV, ads spend, CAC or ROAS through public APIs.

### Initial usage recommendation

- Use Mercado Libre API first for:
  - category discovery;
  - keyword search snapshots;
  - listing snapshots;
  - seller snapshots;
  - reviews/questions where available;
  - trends as secondary discovery signal.
- Persist normalized fields needed for Gate 1–2 plus raw payload.
- Build imports as idempotent `SnapshotRun`s.

## Nubimetrics capability research — initial findings

Sources consulted:

- https://nubimetrics.com/
- https://nubimetrics.com/producto/mercado
- https://nubimetrics.com/producto/competencia
- https://nubimetrics.com/producto/negocio
- https://enterprise.nubimetrics.com/es
- https://nubimetrics.com/api/ returned 404 at time of research.

### Publicly advertised capabilities

Nubimetrics claims to provide, through product/dashboard modules:

- category opportunities;
- searched keywords by category;
- estimated billing and units sold for keywords/categories;
- offer analysis for keyword/product;
- sellers offering a product;
- average price and positioning;
- category sales, monthly growth and seasonality;
- leading sellers and official stores;
- competitor sales in money/units, visits and conversion;
- publication changes over time;
- top publications, average ticket, free shipping incidence, discounts and ranking;
- exports/downloads in some business contexts, especially own transactions in “Mi Negocio”.

### Integration conclusion

- No public API documentation found yet.
- Treat Nubimetrics as high-value external research source, but not as an automated integration until API/export mechanisms and contract restrictions are confirmed.
- For v1, likely options are:
  1. dashboard/manual evidence capture;
  2. structured manual entry of key Nubimetrics metrics;
  3. CSV/XLS export import if plan supports exports;
  4. API integration only if officially available and contractually allowed.

### When dashboard-only is acceptable

- Early Gate 1 screening.
- Occasional qualitative/strategic evidence.
- Metrics that are reviewed manually before decision.
- When export/API is unavailable or contractually unclear.

### When exports/imports are preferable

- Repeated Gate 2 studies.
- Need to compare periods/categories.
- Need reproducible calculations inside E-commerce OS.
- Need to link decisions to source snapshots.

### When API integration is justified

- Officially supported API exists.
- Contract allows storage/processing.
- Data updates frequently enough to justify automation.
- Same data is needed across many candidates/research studies.

## Capturing garbage

“Capturing garbage” means accepting information that creates storage and UI workload but does not improve a gate decision.

Examples:

- vague candidate names such as “cosas para cocina”;
- keywords that are too broad to produce comparable products;
- links without observed date/source/context;
- screenshots without source URL or explanation;
- notes like “parece bueno” without evidence;
- evidence not tied to Gate 1 or Gate 2 questions;
- AI/manual conclusions without observed/calculated inputs;
- copied metrics without period/category/source;
- market research without definition of comparable products.

Guardrail: every candidate/evidence item should answer “what decision does this help?” and “where did this come from?”.

## Initial Gate 1 rubric

Gate 1 question: ¿vale la pena investigar este producto?

### PASS

- Candidate is specific enough to research.
- There is at least one plausible local demand signal.
- Preliminary Mercado Libre category/keyword is identifiable.
- There is an initial competitive hypothesis.
- No obvious blocker makes research pointless.

### HOLD

- Product idea may be interesting but is underspecified.
- Keyword/category is unclear.
- Demand signal is weak or unverified.
- Risk screen found unresolved concerns.
- Needs small additional research before Gate 2.

### REJECT

- Candidate is too vague or not commercially actionable.
- No credible demand signal.
- Obvious blocker: regulation/IP/fragility/weight/warranty/MOQ/etc.
- No credible way to compete can be stated.

## Initial Gate 2 rubric

Gate 2 question: ¿existe demanda suficiente y oportunidad competitiva razonable para justificar sourcing serio?

### PASS

- Market comparable definition is clear.
- Primary/secondary keywords produce relevant comparable listings.
- Demand evidence is sufficient for the level of risk being considered.
- Pricing distribution shows plausible commercial room.
- Market structure is not obviously impossible to enter.
- Top sellers/catalog/official stores are understood.
- Pain points or differentiation angle support a competitive hypothesis.
- Risks are explicit and acceptable for moving to sourcing research.

### HOLD

- Data sample is insufficient or inconsistent.
- Demand exists but magnitude/quality is unclear.
- Competition may be strong but not conclusively disqualifying.
- Product comparability is ambiguous.
- Need Nubimetrics/export/manual validation before sourcing.
- There are unresolved risks that require targeted research.

### REJECT

- Demand signal is too weak for sourcing.
- Relevant market is too small for target sales assumptions.
- Pricing makes a viable imported offer unlikely.
- Dominant sellers/official stores/catalog concentration make entry unattractive.
- Customer pain points do not suggest a realistic differentiation angle.
- Risk profile makes the product unsuitable before sourcing.
