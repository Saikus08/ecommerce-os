# E-commerce OS — Project Context

## Propósito

E-commerce OS es un sistema interno para ayudar a investigar productos, operar y tomar decisiones sobre un negocio de e-commerce en Uruguay.

El objetivo principal no es construir SaaS ni software sofisticado. El objetivo es construir un e-commerce rentable.

El sistema debe:

- reducir incertidumbre;
- organizar investigación;
- integrar información relevante;
- automatizar trabajo repetitivo;
- mantener trazabilidad;
- mejorar decisiones de inversión de tiempo y capital.

## Pregunta rectora

Para cualquier feature:

> ¿Qué decisión concreta del e-commerce mejora?

Si no hay una decisión concreta, probablemente no se debe construir todavía.

## Stack

- Ruby on Rails.
- PostgreSQL.
- React integrado en Rails.
- Railway posteriormente.

Preferencias:

- Rails conventions.
- Modular monolith.
- ActiveRecord idiomático.
- PostgreSQL como source of truth.
- Librerías maduras.
- Soluciones simples.
- Boundaries claros solo donde aportan.
- Prácticas correctas antes que atajos rápidos.

## No objetivos iniciales

- Microservicios.
- Kafka.
- Kubernetes.
- CQRS complejo.
- Event sourcing.
- Data lake.
- Spark.
- Vector database sin caso concreto.
- Multi-tenancy.
- Generic workflow engines.
- Plataforma de agentes.
- Abstracciones Shopify/Amazon.
- Arquitectura enterprise ceremonial.

## Scope actual

Solo implementar correctamente:

1. Gate 1 — Product Candidate Screening.
2. Gate 2 — Market Research.

Sourcing, importación, unit economics, inventario y operación comercial vienen después de tener candidatos que pasen ambos gates.

## Decisiones arquitectónicas iniciales aceptadas

- Rails full-stack con React integrado, no API-only separado inicialmente.
- Modelo normalizado + `raw_payload` JSONB para datos externos.
- Separar `ExternalListing`, `ListingSnapshot` y `SearchResultSnapshot`.
- Incluir `Seller` / `SellerSnapshot` desde el inicio de Gate 2.
- Usar `GateDecision` genérico para soportar gates futuros, implementando solo Gate 1–2 ahora.
- No implementar análisis IA todavía.

## Provenance

Cada dato o conclusión relevante debe poder clasificarse como:

- `OBSERVED` — dato observado desde fuente/manual/API/export.
- `CALCULATED` — resultado determinístico a partir de inputs conocidos.
- `INFERRED` — conclusión interpretativa o asistida.

Guardar cuando aplique:

- source;
- external identifier;
- source URL/reference;
- observed_at;
- acquisition method;
- raw payload o referencia suficiente;
- inputs usados para cálculos/inferencias.

No construir data lineage enterprise. Construir la trazabilidad necesaria para responder: “¿de dónde salió este dato y por qué decidimos esto?”.
