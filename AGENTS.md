# E-commerce OS — Agent Harness

Gobierna cómo los agentes trabajan en este repositorio. El producto existe para ayudar a construir un e-commerce rentable en Uruguay; no para construir software por entusiasmo técnico.

## Prioridad del proyecto

1. Mejorar decisiones reales del e-commerce.
2. Reducir incertidumbre con evidencia trazable.
3. Construir solamente lo necesario para el gate vigente.
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

- Crear harness, contexto, OpenSpec y ADRs iniciales.
- Discutir arquitectura de Gate 1 y Gate 2.
- No implementar dominio sustancial sin spec/ADR aprobado.
- No ejecutar `rails new` sin OK humano explícito.
- No integrar APIs externas, usar datos reales, secretos, cloud o scraping sin decisión explícita.

## Gates funcionales del negocio

1. Product Candidate Screening — ¿vale la pena investigar este producto?
2. Market Research — ¿existe demanda suficiente y oportunidad competitiva razonable?
3. Sourcing — ¿podemos conseguirlo en condiciones aceptables?
4. Import & Compliance — ¿podemos importarlo/comercializarlo legalmente en Uruguay?
5. Unit Economics — ¿es rentable después de costos reales?
6. Investment / Purchase Decision — ¿cuánto capital arriesgamos y hacemos GO/HOLD/NO-GO?
7. Market Validation — ¿el desempeño real valida la hipótesis?
8. Inventory Decision — KILL / REORDER / SCALE.

Implementación actual: solo Gate 1 y Gate 2. Los demás gates pueden existir como conceptos, no como módulos completos.

## Principios de datos

- Esta es una data-intensive application, no una Big Data application.
- PostgreSQL debe alcanzar inicialmente.
- Mantener historia mediante snapshots donde el dato cambie con el tiempo.
- Guardar datos normalizados para consultar/calcular y `raw_payload` para trazabilidad.
- Distinguir datos `OBSERVED`, `CALCULATED` e `INFERRED`.
- La IA puede asistir análisis, pero no tomar decisiones ni establecer hechos. No implementar `AiAnalysis` todavía.

## Integraciones

- Mercado Libre y Nubimetrics deben investigarse antes de diseñar contratos finales.
- Separar capacidades públicas, autenticadas, de cuenta propia y no disponibles.
- No asumir que Nubimetrics tiene API.
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
- No introducir malas prácticas ni atajos técnicos para avanzar más rápido; si la forma correcta requiere más trabajo, explicarlo y pedir decisión.
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
