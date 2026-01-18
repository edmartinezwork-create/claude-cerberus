# CLAUDE.pinescript.md

## Scope
This document applies **only** to Pine Script v6 code written for TradingView.
It overrides any TypeScript, React, or web application standards.
If a rule conflicts with official Pine Script v6 documentation, the official documentation takes precedence.

---

## Language Standards
- Always use **Pine Script version 6** (`//@version=6`)
- Follow the **TradingView Pine Script v6 Reference Manual** strictly
- Declare variables in the **correct scope**. Do not rely on implicit scope promotion
- Avoid global state unless required. Prefer local or `var` scoped variables
- Do not reuse identifiers across incompatible scopes
- All identifiers must be declared before use
- Avoid magic numbers. Use named constants where possible

---

## Structural Rules
- Keep functions under **50 lines**
- Break complex logic into smaller helper functions
- Separate logic into clear sections:
  - Constants
  - Inputs
  - Utility functions
  - Core calculations
  - Drawing logic
  - State management
- Use clear section headers with consistent formatting

---

## Performance Rules
- Minimize loops. Never loop over bars unless unavoidable
- Never nest loops unless mathematically required
- Use `var` to persist values across bars
- Use `barstate.islast` or `barstate.isconfirmed` for expensive operations
- Avoid recalculating values that can be cached
- Limit use of `request.security()` and always document why it is required
- Avoid drawing excessive objects. Respect `max_lines_count`, `max_labels_count`, and `max_boxes_count`

---

## Defensive Coding
- Always guard against `na` values
- Validate array sizes before access
- Validate bar index bounds before historical access
- Never assume data exists on the first bars
- Explicitly handle invalidation conditions for drawings and projections

---

## Drawing & Visuals
- All drawings must be:
  - Configurable via inputs
  - Toggleable (on or off)
- Do not hardcode colors, sizes, or line styles
- Use consistent color logic for bullish vs bearish vs neutral
- Labels must support:
  - Size selection
  - Color selection
  - Visibility toggle
- Lines, boxes, and fills must support:
  - Style selection
  - Width selection
  - Visibility toggle

---

## Fibonacci & Levels (if applicable)
- Always label Fibonacci levels numerically
- Ensure levels update correctly on invalidation
- Do not leave orphaned drawings
- Document the retracement or extension logic used
- Avoid overlapping or duplicated levels

---

## State & Scenarios
- Scenario logic must:
  - Explicitly define activation conditions
  - Explicitly define invalidation conditions
- Never allow multiple active scenarios without clear separation
- Old scenarios must be cleaned up on invalidation
- Predictive paths must auto-delete when invalidated

---

## Testing & Validation
Pine Script does not support automated unit tests.
Instead, every change must pass:

- Clean compile with no warnings
- Visual validation on:
  - Low timeframe
  - High timeframe
  - Sparse data symbols
- Manual checklist:
  - No repainting unless explicitly documented
  - No object leaks
  - Inputs behave as expected
  - Toggles actually disable logic, not just visuals

Document testing assumptions in comments if needed.

---

## Git Workflow
- Branch names must follow:
  - `feature/description`
  - `fix/description`
- Commit messages must be descriptive and specific
- Do not commit broken or partially compiling scripts
- Do not merge without manual visual verification

---

## Documentation
- Every script must include a header with:
  - Script name
  - Version
  - Purpose
  - High-level logic description
- Add inline comments for non-obvious logic
- If mimicking a known trading methodology:
  - Name it
  - Describe it
  - Document deviations or assumptions

---

## Common Mistakes to Avoid
- Do not use undocumented Pine behavior
- Do not rely on repainting unless explicitly stated
- Do not exceed object limits
- Do not hide logic behind visuals
- Do not introduce unused inputs or dead code

---

## When Stuck
- Re-check Pine Script v6 documentation
- Reduce the problem to a minimal reproducible script
- Validate scope, order of declarations, and bar state logic
- If adding a workaround, explain **why** in a comment with a TODO tag
