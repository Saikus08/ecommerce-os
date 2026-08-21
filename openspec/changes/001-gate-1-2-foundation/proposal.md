# Change 001 — Gate 1–2 Foundation

## Status

Draft

## Why

E-commerce OS debe ayudar a decidir si un producto merece investigación adicional y, luego, si existe demanda y oportunidad competitiva suficiente para justificar sourcing serio.

La aplicación debe ser un MVP sólido para Gate 1 y Gate 2, extensible a gates posteriores sin implementarlos prematuramente.

## Business decisions improved

1. Gate 1 — Product Candidate Screening: ¿vale la pena investigar este producto?
2. Gate 2 — Market Research: ¿existe demanda suficiente y oportunidad competitiva razonable?

## Scope

In scope:

- Product candidates.
- Gate decisions humanas con outcome, rationale y evidencia.
- Evidence/provenance mínimo.
- Market research studies.
- Mercado Libre/Nubimetrics como fuentes a investigar antes de contrato final.
- External listings, sellers y snapshots temporales.
- Cálculos determinísticos de pricing/market structure cuando existan datos suficientes.
- Jobs para snapshots/imports cuando la sincronización lo justifique.
- Rúbricas explícitas para evitar capturar datos que no mejoran decisiones.

Out of scope:

- Sourcing formal.
- Import & compliance.
- Unit economics.
- Investment/purchase execution.
- Market validation post-publicación.
- Inventory decisions.
- AI analysis model.
- Scraping no aprobado.
- Integraciones externas sin investigación y decisión explícita.

## Initial domain concepts

- `ProductCandidate`: idea de producto a evaluar.
- `MarketResearch`: estudio Gate 2 para un candidato.
- `GateDecision`: decisión humana asociada a un gate.
- `EvidenceItem`: evidencia observada, calculada o inferida.
- `SnapshotRun`: ejecución de captura/importación.
- `ExternalListing`: identidad estable de un listing externo.
- `ListingSnapshot`: estado observado de un listing en un momento.
- `SearchResultSnapshot`: aparición/ranking de un listing en una búsqueda específica.
- `Seller`: identidad estable de un seller externo.
- `SellerSnapshot`: estado observado de un seller en un momento.

## Open questions

- Test runner: RSpec.
- Versiones: usar versiones modernas recomendadas y disponibles localmente para Rails 8+ y Node 24+; fijar explícitamente en archivos del proyecto para reproducibilidad.
- Mercado Libre: investigación inicial documentada en `design.md`; hay endpoints útiles para categorías, búsquedas, ítems, sellers, tendencias, reviews y preguntas. Falta validar en práctica qué requiere autenticación y qué datos reales expone para Uruguay.
- Nubimetrics: investigación inicial documentada en `design.md`; no se encontró API pública documentada. Tratar como dashboard/manual/export hasta confirmar contrato/API.
- “Capturar basura” significa aceptar candidatos/evidencia sin estructura mínima para decidir: nombres vagos, keywords no accionables, notas sin fuente, datos sin fecha, screenshots/links sin contexto, hipótesis no falsables o evidencia no vinculada a una pregunta de gate.
- Gate 2 debe poder recomendar PASS/HOLD/REJECT solo cuando haya definición de mercado comparable, fuente/periodo analizado, muestra competitiva suficiente para la decisión, señales de demanda documentadas, pricing/market structure calculados sobre datos disponibles, riesgos explícitos y rationale humano trazable.

## Gate 1 data quality guardrails

Para evitar capturar basura, un Product Candidate no debería avanzar si no tiene al menos:

- nombre suficientemente específico;
- descripción breve del producto;
- origen de la idea;
- categoría o categoría tentativa de Mercado Libre;
- keyword primaria preliminar;
- al menos una señal inicial de demanda o razón de investigación;
- opportunity hypothesis en forma: “Creemos que podemos competir porque ...”;
- riesgos obvios revisados, aunque sea para indicar “no observado todavía”.

## Gate 2 minimum decision criteria

Una decisión Gate 2 debe distinguir:

### PASS

Se puede justificar sourcing serio cuando existe evidencia suficiente de demanda local, estructura competitiva abordable, rango de precios observable, ausencia de blockers obvios para continuar, y una hipótesis competitiva plausible.

### HOLD

Se usa cuando la oportunidad no está descartada pero falta evidencia material, la muestra es insuficiente, los datos son contradictorios, la categoría/keyword comparable no está clara, o hay riesgos que requieren investigación antes de sourcing.

### REJECT

Se usa cuando la evidencia muestra demanda insuficiente, competencia estructuralmente desfavorable, precios incompatibles con una oportunidad razonable, concentración dominante difícil de atacar, blockers obvios, o falta de hipótesis competitiva creíble.
