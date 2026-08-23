# Política human-in-the-loop

## Principio

El agente puede investigar, proponer y ejecutar cambios locales reversibles dentro de un alcance aprobado. El humano conserva decisiones materiales de negocio, arquitectura, seguridad, gasto, publicación, datos reales y mutaciones externas.

## Requiere OK explícito

- Primer `rails new`.
- Agregar dependencias no previstas.
- Usar secretos o datos reales.
- Integrar sistemas externos.
- Scraping.
- Cloud/Railway/deploy.
- Push/merge/release.
- Migraciones destructivas.
- Cambios materiales de arquitectura.

## Alcance de producto inminente

El producto inminente puede especificar e implementar, con OpenSpec aprobado por slice:

- descubrimiento de oportunidades;
- cuantificación de demanda;
- cuantificación de competencia;
- unit economics;
- score/riesgo explicable;
- decisión GO/REVIEW/NO-GO;
- preparación de sourcing;
- test pequeño;
- señales para escalar/hold/kill.

Esto no autoriza automáticamente datos reales, credenciales, scraping, compras, cloud, ni integraciones externas con mutación.

## Permitido sin OK adicional dentro de esta fase

- Crear documentación de harness.
- Crear OpenSpec/ADR borrador.
- Inspeccionar archivos no secretos.
- Verificar versiones locales.
- Investigar documentación pública de proveedores.
- Crear spikes/specs/ADRs para integraciones y scoring.
