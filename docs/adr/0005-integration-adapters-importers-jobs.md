# ADR-0005 — Integraciones mediante clients, importers y jobs concretos

## Status

Accepted

## Context

Mercado Libre y Nubimetrics pueden aportar valor real a Gate 1 y Gate 2, pero sus capacidades deben investigarse antes de asumir contratos. No queremos scraping frágil ni abstracciones genéricas prematuras.

## Decision

Implementar integraciones por fuente usando piezas concretas:

- clients para HTTP/API/export parsing;
- importers/mappers para convertir respuestas externas a modelos propios;
- jobs para sincronización, retries y snapshots recurrentes;
- `SnapshotRun` e idempotency keys para trazabilidad y reintentos seguros.

No crear un framework genérico de integraciones inicialmente.

## Alternatives

- Abstracción genérica `ExternalProvider` desde el día uno.
- Scripts ad hoc sin modelos de importación.
- Copy/paste manual permanente.
- Scraping sin decisión explícita.

## Consequences

- Integraciones profesionales sin arquitectura enterprise innecesaria.
- Permite tratar diferencias reales entre Mercado Libre y Nubimetrics.
- Requiere investigar capacidades oficiales antes de cerrar specs.
- Jobs recurrentes hacen sentido para snapshots, pero deben ser idempotentes.
