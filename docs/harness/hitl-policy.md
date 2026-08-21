# Política human-in-the-loop

## Principio

El agente puede investigar, proponer y ejecutar cambios locales reversibles dentro de un alcance aprobado. El humano conserva decisiones materiales de negocio, arquitectura, seguridad, gasto, publicación y datos reales.

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

## Permitido sin OK adicional dentro de esta fase

- Crear documentación de harness.
- Crear OpenSpec/ADR borrador.
- Inspeccionar archivos no secretos.
- Verificar versiones locales.
