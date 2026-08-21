# Arquitectura del harness

El harness es el sistema de contexto, decisión y autorización del repositorio. No es el producto.

## Piezas

| Path | Función |
|------|---------|
| `AGENTS.md` | Reglas de trabajo, scope autorizado, gates humanos |
| `openspec/project.md` | Contexto estable del proyecto |
| `openspec/changes/` | Propuestas/specs de cambios materiales |
| `openspec/specs/` | Comportamiento aceptado/documentado |
| `.opencode/context/` | Contexto que debe cargar el agente |
| `docs/adr/` | Decisiones arquitectónicas |
| `docs/project-status.md` | Tarjeta breve de estado |

## Relación con el código

Cuando exista Rails, el código de producto vivirá en la raíz Rails convencional. El harness gobierna el trabajo, pero no debe convertirse en burocracia pesada.
