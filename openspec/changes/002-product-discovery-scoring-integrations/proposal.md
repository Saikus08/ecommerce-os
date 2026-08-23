# Change 002 — Product Discovery, Scoring & Integration Spike

## Status

Draft spike

## Why

E-commerce OS debe pasar de registrar candidatos a soportar un flujo operativo completo para descubrir oportunidades, cuantificar mercado, calcular economics y decidir GO/REVIEW/NO-GO con evidencia trazable.

El objetivo no es crear un score opaco ni automatizar antes de conocer las fuentes. El objetivo es cerrar un modelo de decisión explicable y verificar si Mercado Libre/Nubimetrics pueden aportar los datos necesarios de forma programática, exportable o manual estructurada.

## Business decisions improved

1. ¿Vale la pena investigar esta idea?
2. ¿Existe demanda accesible suficiente para Uruguay?
3. ¿La estructura competitiva permite capturar un market share razonable?
4. ¿Los unit economics son positivos bajo escenarios realistas?
5. ¿Conviene avanzar a sourcing, dejar en revisión o descartar?
6. ¿Qué riesgo/capital justifica un test pequeño antes de escalar?

## Product flow

```text
descubro oportunidad
→ cuantifico demanda
→ cuantifico competencia
→ calculo unit economics
→ asigno score/riesgo explicable
→ GO/REVIEW/NO-GO
→ sourcing
→ test pequeño
→ escalo/hold/kill
```

## Scope of this spike

In scope:

- Specify the end-to-end domain shape from ProductCandidate to decision.
- Define demand, competition, economics, risk and opportunity score formulas.
- Define hard gates that override aggregate score.
- Identify required normalized data and snapshot boundaries.
- Verify Mercado Libre API capabilities for search/listings/sellers/categories and fee/cost calculation.
- Verify Nubimetrics access options: API, CSV/XLS exports, dashboard/manual capture, contract limitations.
- Decide which data can be automated now vs captured manually.
- Produce implementation slices for the next approved changes.

Out of scope for the spike:

- Using real credentials or real private data.
- Scraping.
- Purchases, sourcing execution, supplier negotiation or import execution.
- Cloud/deploy.
- Opaque AI scoring or `AiAnalysis`.
- Building full inventory/reorder automation.

## Initial domain direction

Candidate domain chain:

- `ProductCandidate`
- `MarketResearch`
- `MarketSnapshot`
- `DemandAssessment`
- `CompetitionAssessment`
- `EconomicsScenario`
- `OpportunityAssessment`
- `GateDecision`
- later: `SourcingCandidate`, `SmallTest`, `InventoryDecision`

This is a direction to validate, not permission to implement all models at once.

## Open questions

- What Mercado Libre endpoints are public vs authenticated for Uruguay (`MLU`)?
- Does Mercado Libre expose the fee/cost calculator needed for category/listing/logistics costs in our use case?
- Does Nubimetrics provide an official API, export files, or only dashboard/manual review under available plans?
- What metric definitions does Nubimetrics use for units sold, sales trend, search intent and seasonality?
- How should accessible demand be estimated for small Uruguay markets?
- What initial capital budget thresholds should hard gates use?
- Where does sourcing begin without prematurely implementing full sourcing/import/compliance?
