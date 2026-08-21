# ADR-0004 — GateDecision genérico para gates del negocio

## Status

Accepted

## Context

El negocio tiene ocho gates, pero el alcance inicial solo implementa Product Candidate Screening y Market Research. Queremos evitar sobreconstruir gates futuros, pero no bloquear la evolución.

## Decision

Usar un modelo conceptual `GateDecision` capaz de representar decisiones de los ocho gates, implementando flujos reales solo para Gate 1 y Gate 2 inicialmente.

## Alternatives

- Crear una tabla de decisión distinta por gate.
- Modelar los ocho gates completos desde el inicio.
- Guardar decisiones como notas libres.

## Consequences

- Las decisiones quedan auditables y comparables.
- Evita crear módulos prematuros para Sourcing, Import, Unit Economics e Inventory.
- Requiere validar outcomes según gate para no perder semántica.
