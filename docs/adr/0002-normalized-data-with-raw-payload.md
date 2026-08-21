# ADR-0002 — Datos normalizados con raw payload

## Status

Accepted

## Context

Gate 1 y Gate 2 dependen de datos externos y manuales que deben ser consultables, calculables y auditables. También necesitamos conservar la respuesta original para trazabilidad y re-procesamiento futuro.

## Decision

Guardar campos normalizados para datos usados en consultas, cálculos y decisiones, y conservar además `raw_payload` JSONB cuando provengan de fuentes externas o importaciones relevantes.

## Alternatives

- Guardar todo como JSONB.
- Modelar todo altamente normalizado desde el inicio.
- Guardar solo estado actual sin payload original.

## Consequences

- Permite cálculos determinísticos y queries eficientes.
- Conserva provenance suficiente.
- Evita sobre-modelar campos todavía no usados.
- Requiere disciplina para decidir qué se normaliza y qué queda solo en payload.
