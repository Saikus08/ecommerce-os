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
| `.opencode/agents/` | Agentes especializados para Rails, frontend, seguridad y evaluación |
| `.opencode/skills/` | Playbooks de trabajo para implementación, testing, DB, frontend y discovery |
| `opencode.json` | Permisos locales de herramientas/agentes |
| `docs/adr/` | Decisiones arquitectónicas |
| `docs/project-status.md` | Tarjeta breve de estado |

## Relación con el código

El código de producto vive en la raíz Rails convencional. El harness gobierna el trabajo, pero no debe convertirse en burocracia pesada.

## Regla operativa

El harness existe para acelerar desarrollo profesional con trazabilidad: specs chicas, branches por slice, evidencia ejecutable, revisión independiente para cambios materiales y gates humanos donde hay riesgo real.
