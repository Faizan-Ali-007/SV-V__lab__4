# Delivery Robot — State Transition Table

| Transition_id | From_state | Event | To_state | Requirements |
|----------------|------------|-------|----------|----------------|
| T1 | IDLE | Delivery Request Received | NAVIGATING | R2 |
| T2 | NAVIGATING | Obstacle Detected | AVOIDING_OBSTACLE | R4 |
| T3 | AVOIDING_OBSTACLE | Obstacle Avoided | NAVIGATING | R5 |
| T4 | NAVIGATING | Destination Reached | DELIVERING | R6 |
| T5 | NAVIGATING | Critical Battery | RETURNING | R9 |
| T6 | DELIVERING | Delivery Successful | RETURNING | R7 |
| T7 | RETURNING | Warehouse Reached | IDLE | R10 |

Any state/event combination not listed above is an **undefined (invalid) transition** and must not occur in the implementation.

---

## Verification Activity

### Check 1 — Invalid Transition: IDLE → DELIVERING
**Can this happen?** No.
**Requirement violated:** R2 and R6. R2 allows IDLE to transition only to NAVIGATING (on a delivery request). R6 requires "Destination Reached" — which can only occur from NAVIGATING — before entering DELIVERING. A direct IDLE → DELIVERING jump has no corresponding transition and would mean delivering without ever confirming arrival.

### Check 2 — Missing Transition: NAVIGATING → AVOIDING_OBSTACLE with no path back
**Problem:** This is a deadlock. T3 (AVOIDING_OBSTACLE → NAVIGATING on Obstacle Avoided) is required by R5. If T3 is missing, the robot is permanently stuck in AVOIDING_OBSTACLE.
**Can the robot continue its delivery?** No — it can never resume navigation or reach the destination.

### Check 3 — Obstacle During Delivery: AVOIDING_OBSTACLE → DELIVERING directly
**Can this happen?** No.
**Reasoning:** No transition authorizes this. The only valid path is T3 (AVOIDING_OBSTACLE → NAVIGATING) followed by T4 (NAVIGATING → DELIVERING, on Destination Reached).

---

## Summary of Findings

| Issue | Type | Severity |
|-------|------|----------|
| IDLE → DELIVERING | Invalid transition | Critical |
| No return path from AVOIDING_OBSTACLE (missing T3) | Missing transition / Deadlock | Critical |
| AVOIDING_OBSTACLE → DELIVERING | Invalid transition | Critical |
