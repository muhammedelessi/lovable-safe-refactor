# Safe Refactor Playbook

## Batch design

A batch should have one coherent objective. Good examples:

- split one oversized page into presentation and data-access responsibilities
- consolidate duplicate API calls for one domain operation
- remove one obsolete abstraction after proving no callers remain
- move one feature's business logic into a cohesive module
- normalize error handling for one integration boundary

Bad batch: "clean the entire src folder".

## Before editing

Capture the baseline:

- affected behavior
- public component/function signatures
- route/API/database contracts
- relevant tests/build status
- direct callers and consumers

If baseline verification is already failing, record that before refactoring so old failures are not mistaken for regressions.

## During editing

Keep behavior-preserving changes separate from functional changes. If a functional change becomes necessary, stop and request approval rather than smuggling it into the refactor.

Prefer mechanically understandable transformations. Avoid large renames, broad formatting churn, dependency upgrades, and architecture changes in the same batch.

Do not introduce a dependency merely to reduce a small amount of local code. Reuse current project conventions when they are sound.

## After editing

Run focused verification first, then broader checks. Inspect the final diff for accidental behavior changes, unrelated cleanup, removed edge cases, changed strings, route changes, contract changes, and secret/config modifications.

If verification fails:

1. Stop the sequence.
2. Determine whether failure existed before the batch.
3. If introduced by the batch, fix or revert within the approved scope.
4. If the solution requires broader behavior change, ask for approval.

## Refactor completion report

Report:

- batch objective
- changed files/modules
- structural improvement
- preserved contracts
- verification performed and result
- unresolved risks
- suggested next batch

Do not begin the suggested next batch until approval is clear when it materially expands scope.
