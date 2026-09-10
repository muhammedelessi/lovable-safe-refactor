# Audit and Refactor Report Format

Use this default format and keep it concise enough to drive action.

# Lovable Refactor Audit

## Executive summary
State overall technical-debt level, highest-risk areas, and whether refactoring can proceed incrementally.

## Architecture map
Summarize relevant modules, data flow, integrations, and protected boundaries.

## Findings
For each meaningful finding provide:

- **Severity:** Critical / High / Medium / Low
- **Evidence:** file/module and concrete pattern
- **Impact:** why this matters
- **Blast radius:** likely affected callers/features
- **Recommendation:** smallest safe direction
- **Preserve:** behavior/contracts that must not change
- **Verify:** checks needed after refactor
- **Approval:** whether protected-boundary approval is required

Avoid filling the report with cosmetic findings.

## Proposed batches
Order batches so early work reduces risk for later work. Keep each batch independently reviewable and reversible where practical.

For each batch state objective, approximate scope, risk, verification, and dependencies.

## Approval gate
End with the exact first batch you recommend and request explicit approval before modifying code.

# After an approved batch

Report:

- objective completed
- files/modules changed
- behavior/contracts preserved
- verification result
- regressions or residual risk
- next recommended batch
