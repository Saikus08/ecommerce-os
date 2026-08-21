# ADR-0003 — Entidades externas y snapshots temporales

## Status

Accepted

## Context

Precios, rankings, promociones, reviews, sellers y datos competitivos cambian con el tiempo. Gate 1 y Gate 2 requieren ver el estado observado y preservar historia.

## Decision

Separar identidad externa estable y observaciones temporales:

- `ExternalListing` identifica un listing externo.
- `ListingSnapshot` guarda el estado observado del listing en un momento.
- `SearchResultSnapshot` guarda aparición, posición y contexto dentro de una búsqueda.
- `Seller` identifica un seller externo.
- `SellerSnapshot` guarda datos cambiantes del seller.

## Alternatives

- Guardar solo el último estado.
- Guardar snapshots sin entidad externa estable.
- Poner posición/ranking dentro del listing.

## Consequences

- Permite historia y análisis temporal.
- Evita confundir atributos del listing con atributos de una búsqueda.
- Facilita idempotencia por `SnapshotRun` y claves externas.
- Agrega algunas tablas y joins, pero justificados por Gate 2.
