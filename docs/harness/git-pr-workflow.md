# Flujo local de Git y propuestas de cambio

`AGENTS.md` manda sobre alcance y gates. Este runbook fija la secuencia local.

## Reglas

- `main` no recibe trabajo directo.
- Una branch = una capacidad, incidente, spike o cambio de proceso.
- Prefijos sugeridos: `feature/`, `fix/`, `chore/`, `spike/`.
- Árbol e índice limpios antes de cambiar de rama o abrir una slice, salvo que se use un worktree separado para aislar trabajo en curso.
- Commits atómicos; paths aprobados declarados antes del stage.
- Push, PR, merge remoto, rebase, force-push y deploy requieren OK humano.

## Empezar una slice

1. Revisar `git status --short --branch`.
2. Si hay cambios no relacionados, parar o crear worktree separado desde la base correcta.
3. Crear branch desde `main` actualizado: `git switch -c <prefix>/<nombre>`.

## Commit local

1. Declarar paths aprobados.
2. Stagear solo esos paths; evitar `git add .`.
3. Verificar que el índice coincide exactamente con lo aprobado.
4. Commit con mensaje que explique el porqué.

## Merge local

Permitido cuando la persona lo pide explícitamente y el diff/checks fueron revisados. No implica push remoto.
