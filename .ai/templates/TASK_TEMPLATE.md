# Task Graph — [Feature]

## Dependency Graph

```text
TASK-001 → TASK-002 → TASK-004
              └────→ TASK-003 ─┘
```

## TASK-001 — [Goal]

- Status: TODO
- Depends on: None
- Requirements: REQ-001
- API: API-001 / N/A
- Design: DESIGN-001 / N/A
- Acceptance: AC-001

### Expected files

- `src/...`

### Implementation

One concrete, bounded change.

### Verification

- lint/typecheck as applicable
- TEST-001 / E2E-001 / VISUAL-001

### Done when

- implementation complete
- required checks actually pass
- AC evidence exists

## Progress

| Task | Status | REQ | AC | Verification |
|---|---|---|---|---|
| TASK-001 | TODO | REQ-001 | AC-001 | TEST-001 |

Allowed: `TODO / IN_PROGRESS / BLOCKED / DONE`.
