---
name: ecommerce-product-discovery
description: Evaluate E-commerce OS product discovery, demand, competition, unit economics, opportunity scoring, risk, GO/NO-GO, sourcing, small-test, and scale decisions.
compatibility: opencode
---

# E-commerce Product Discovery

Use when designing or reviewing the product-discovery domain, scoring formulas, market research, economics, sourcing readiness, and decision gates.

## Operating Chain

The product flow is:

1. Discover opportunity.
2. Quantify demand.
3. Quantify competition.
4. Calculate unit economics.
5. Assign explainable score and risk.
6. Decide GO/REVIEW/NO-GO.
7. Source.
8. Run a small test.
9. Scale, hold, reorder, or kill.

## Non-Negotiables

- No opaque AI score.
- Scores must be formula-driven and explainable.
- Hard gates override aggregate score.
- Uruguay is a small market; absolute volume thresholds must be calibrated.
- Prefer accessible demand over raw demand: monthly demand × realistically capturable market share.
- Ask: can we sell a reasonable initial lot in <= 90 days capturing roughly 3-10% of the market?

## Demand Score Draft

0 to 100, based primarily on Nubimetrics/Mercado Libre evidence:

- 35% monthly units sold.
- 25% search volume / purchase intent.
- 20% 90/180-day sales trend.
- 20% stability vs seasonality.

## Competition Score Draft

0 to 100, where 100 means attractive market:

- 30% sales per seller/listing: supply vs demand.
- 25% Top 5 / Top 10 sales concentration.
- 20% Mercado Líder / dominant seller concentration.
- 15% catalog participation.
- 10% price pressure / product homogeneity.

## Economics

Do not start with an economics score. Start with real numbers:

- Contribution profit/unit.
- Contribution margin %.
- Break-even ROAS.
- ROI on lot.
- Capital required.
- Months to recover inventory.
- Sensitivity: price -10%, landed cost +15%, CAC +30%.
- Scenarios: optimistic, base, stress.

## Opportunity Score Draft

Only after demand, competition and economics are calculated:

- 30% Demand.
- 25% Competition.
- 30% Economics.
- 15% Risk / Operational Fit.

Risk / Operational Fit includes size/weight, fragility, regulation/certifications, returns, warranty, variant complexity, MOQ, and capital required.

## Hard Gates Draft

- Insufficient demand -> NO-GO.
- Negative economics -> NO-GO.
- Capital required above budget -> NO-GO.
- Critical regulatory/logistics risk -> NO-GO.
- Score >= 70 with no hard fails -> GO.
- Score 55-69 -> REVIEW.
- Score < 55 -> NO-GO.

Thresholds are initial parameters and must be calibrated with real candidates.

## Integration Caution

- Nubimetrics offers relevant business information, but API/export access must be verified before designing ingestion.
- Mercado Libre API/cost endpoints must be validated for Uruguay, category, listing type, logistics, auth, and limits.
- Do not design ingestion around assumed payloads.
