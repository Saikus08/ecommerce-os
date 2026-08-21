# Project Context — E-commerce OS

## Resumen

Sistema interno para investigar productos y tomar mejores decisiones para un e-commerce en Uruguay. El producto acompaña una operación real: descubrir oportunidades, investigar Mercado Libre Uruguay, validar demanda/competencia, luego sourcing/importación/unit economics y decisiones de inventario.

## Estado actual

Rails ya fue creado como aplicación full-stack con PostgreSQL y esbuild. Hay harness/OpenSpec/ADRs iniciales. Todavía no hay dominio implementado.

## Scope vigente

- Gate 1: Product Candidate Screening.
- Gate 2: Market Research.

No construir gates posteriores aún, salvo preparar `GateDecision` para representarlos conceptualmente.

## Decisiones aceptadas

- Rails full-stack + React integrado.
- PostgreSQL source of truth.
- Modular monolith.
- Modelo normalizado + JSONB raw payload.
- Entidades externas + snapshots temporales.
- `ExternalListing` identifica un listing externo estable.
- `ListingSnapshot` captura estado observado del listing.
- `SearchResultSnapshot` captura aparición/ranking en una búsqueda específica.
- `Seller` y `SellerSnapshot` son necesarios para estructura competitiva.
- No `AiAnalysis` todavía.

## Preguntas abiertas relevantes

- Versión final de Ruby/Rails/Node a fijar para compatibilidad con Railway y gems.
- Estructura exacta de React dentro de Rails.
- Test runner inicial: RSpec.
- Capacidades reales de Mercado Libre API para Gate 1–2.
- Capacidades reales de Nubimetrics: API, exports, restricciones contractuales.
- PostgreSQL local requiere credenciales; `db:prepare` está bloqueado hasta configurar acceso local vía entorno/rol.

## Riesgos

- Construir demasiado antes de validar candidatos reales.
- Asumir datos que Mercado Libre/Nubimetrics no exponen.
- Sobre-modelar gates futuros.
- Introducir infraestructura de Big Data innecesaria.
