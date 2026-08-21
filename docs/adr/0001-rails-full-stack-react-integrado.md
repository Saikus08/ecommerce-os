# ADR-0001 — Rails full-stack con React integrado

## Status

Accepted

## Context

E-commerce OS necesita una aplicación interna sólida para investigación y toma de decisiones. El stack objetivo es Rails, PostgreSQL y React, evitando complejidad de infraestructura innecesaria.

## Decision

Usar Rails como aplicación principal full-stack y montar React dentro de Rails para las pantallas que necesiten interacción rica.

No iniciar como Rails API-only + SPA separada.

## Alternatives

- Rails API-only + React/Vite separado.
- Rails con Hotwire sin React.
- Next.js separado + Rails API.

## Consequences

- Deployment más simple.
- Menos complejidad de auth, CORS y routing duplicado.
- Rails mantiene control de routing, sesiones futuras, ActiveRecord y jobs.
- React se usa donde aporta experiencia interactiva.
- Si el frontend crece mucho, habrá que cuidar organización dentro de `app/javascript`.
