---
name: frontend-react-workflow
description: Build E-commerce OS React-in-Rails frontend slices for candidate screening, market research, scoring, economics, and decision workflows.
compatibility: opencode
---

# Frontend React Workflow

Use for React/UI changes inside the Rails app.

## Boundaries

- Frontend is UI and interaction state; authoritative decisions and calculations stay server-side unless explicitly specified.
- No server secrets in JavaScript.
- No direct database access.
- Do not invent backend permissions, fields, scores, or decision outcomes not supported by the API/spec.

## Product UX Rules

- Optimize for decisions, not dashboards for their own sake.
- Make evidence, assumptions, hard-gate failures, and calculation inputs visible.
- Keep flows explicit: candidate -> market validation -> economics -> risk/score -> GO/REVIEW/NO-GO -> sourcing/test/scale.
- Handle loading, success, empty, error, unauthorized, and validation states when relevant.
- Avoid hiding uncertainty behind visual polish.

## Implementation

- Follow existing Rails asset/build structure.
- Prefer clear state and small components over premature abstraction.
- Keep API error handling aligned with backend shape.
- Do not add UI libraries before a concrete need.

## Verification

Use the project frontend runner once established. Until then, report missing runner as justified `N/A` and verify with available build/type/lint commands if present.
