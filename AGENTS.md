# E-commerce OS — Agent Harness

Gobierna cómo los agentes trabajan en este repositorio. El producto existe para ayudar a construir un e-commerce rentable en Uruguay; no para construir software por entusiasmo técnico.

## Prioridad del proyecto

1. Mejorar decisiones reales del e-commerce.
2. Reducir incertidumbre con evidencia trazable.
3. Construir slices pequeños orientados al próximo riesgo/decisión.
4. Mantener Rails idiomático, PostgreSQL como source of truth y arquitectura simple.

Pregunta obligatoria para cualquier feature:

> ¿Qué decisión concreta del e-commerce mejora?

## Stack objetivo

- Ruby on Rails.
- PostgreSQL.
- React integrado dentro de Rails.
- Railway posteriormente.
- Modular monolith, no microservicios.

## Alcance actual autorizado

- Crear y mejorar harness, contexto, OpenSpec y ADRs.
- Diseñar e implementar slices aprobados para convertir ideas en decisiones GO/REVIEW/NO-GO.
- No implementar dominio sustancial sin spec/ADR aprobado.
- No integrar APIs externas con credenciales/datos reales, usar secretos, cloud o scraping sin decisión explícita.

## Gates funcionales del negocio

1. Product Candidate Screening — ¿vale la pena investigar este producto?
2. Market Research — ¿existe demanda suficiente y oportunidad competitiva razonable?
3. Sourcing — ¿podemos conseguirlo en condiciones aceptables?
4. Import & Compliance — ¿podemos importarlo/comercializarlo legalmente en Uruguay?
5. Unit Economics — ¿es rentable después de costos reales?
6. Investment / Purchase Decision — ¿cuánto capital arriesgamos y hacemos GO/HOLD/NO-GO?
7. Market Validation — ¿el desempeño real valida la hipótesis?
8. Inventory Decision — KILL / REORDER / SCALE.

Producto inminente: descubrimiento de oportunidad → cuantificación de demanda → cuantificación de competencia → cálculo de unit economics → score/riesgo explicable → GO/REVIEW/NO-GO → sourcing → test pequeño → escalar/hold/kill.

Los gates posteriores pueden especificarse e implementarse por slices aprobados cuando reduzcan incertidumbre real. No construir operación completa ni automatización especulativa antes de validar datos/fuentes.

## Principios de datos

- Esta es una data-intensive application, no una Big Data application.
- PostgreSQL debe alcanzar inicialmente.
- Mantener historia mediante snapshots donde el dato cambie con el tiempo.
- Guardar datos normalizados para consultar/calcular y `raw_payload` para trazabilidad.
- Distinguir datos `OBSERVED`, `CALCULATED` e `INFERRED`.
- La IA puede asistir análisis, pero no tomar decisiones ni establecer hechos. No implementar `AiAnalysis` opaco. Scores deben ser fórmulas explicables y testeadas.

## Scoring y decisiones

- No inventar un “AI score” opaco.
- Demand Score, Competition Score, Economics y Opportunity Score deben tener inputs, pesos y outputs trazables.
- Unit economics empieza con números financieros reales, no con score.
- Hard gates prevalecen sobre scores agregados: demanda insuficiente, economics negativos, capital superior a presupuesto o riesgo crítico implican NO-GO.
- Los umbrales iniciales se calibran con candidatos reales, no se tratan como verdad permanente.

## Integraciones

- Mercado Libre y Nubimetrics deben investigarse antes de diseñar contratos finales.
- Separar capacidades públicas, autenticadas, de cuenta propia y no disponibles.
- No asumir que Nubimetrics tiene API.
- Validar endpoint/calculador de costos de Mercado Libre antes de automatizar comisiones/logística.
- No implementar scraping frágil sin discusión.
- Usar clients/adapters/importers concretos por fuente, no framework genérico de integraciones.

## Jerarquía de contexto

1. Instrucciones humanas de la sesión.
2. Este archivo.
3. `openspec/project.md`.
4. Specs activas en `openspec/changes/`.
5. ADRs aceptadas en `docs/adr/`.
6. Código.

Ante contradicción, parar y registrar la decisión necesaria.

## Forma de trabajo

- Proponer → especificar → decidir → implementar → verificar.
- Para cambios materiales, crear OpenSpec antes de codear.
- Mantener cambios chicos y revisables.
- Usar documentación oficial actualizada vía Context7 para Rails/React/librerías.
- Usar skills/agentes de `.opencode/` cuando aporten foco: Rails, DB, frontend, testing, seguridad, evaluación y product discovery.
- No introducir malas prácticas ni atajos técnicos para avanzar más rápido; si la forma correcta requiere más trabajo, explicarlo y pedir decisión.
- `main` no es rama de trabajo; usar branch por slice/spike según `docs/harness/git-pr-workflow.md`.
- No leer `.env` ni secretos.
- No hacer push, deploy, cloud, migraciones destructivas o integración externa sin OK humano explícito.

## Comunicación

Responder en español, con foco en producto y decisión. Preferir:

```text
Ahora: ...
Bloqueado: ...
Siguiente: ...
Pedido a vos: ...
Riesgo: ...
```
