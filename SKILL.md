---
name: lovable-safe-refactor
description: "Safely audit and incrementally refactor existing Lovable projects that have grown messy, duplicated, fragile, or inconsistently structured. Use when asked to clean up, reorganize, modernize, reduce technical debt, split oversized components, remove duplication, improve maintainability, or repair architecture in a Lovable-built project. First audit and map the current system without changing code, then present a prioritized plan and stop for explicit approval. After approval, refactor in small reversible batches while preserving UI, behavior, routes, APIs, Supabase contracts, authentication, RLS, and production data unless the user explicitly approves those changes."
---

# Lovable Safe Refactor

Refactor legacy Lovable projects without turning cleanup into a rewrite.

## Non-negotiable workflow

Follow this sequence:

1. **Audit** the existing project without modifying code.
2. **Map** architecture, dependencies, data flow, integrations, and risky boundaries.
3. **Prioritize** refactor opportunities by risk and value.
4. **Present** the plan, affected surfaces, and rollback strategy.
5. **STOP and wait for explicit approval.**
6. After approval, **refactor one small batch at a time**.
7. **Build/test/verify after every batch** before moving on.
8. **Re-review** the touched area and report remaining risk.

Never skip the approval gate because the request says "clean everything", "refactor the whole app", or similar.

## Phase 1: Audit only

Read [references/audit-framework.md](references/audit-framework.md).

Inspect enough of the project to understand the real architecture before judging isolated files. Start from project manifests, routing, entry points, shared UI, feature areas, state/data access, integrations, and tests. Trace callers and consumers before proposing moves or interface changes.

During the audit:

- Do not edit, rename, move, delete, reformat, or generate production files.
- Distinguish proven problems from preferences.
- Prefer evidence from code paths, imports, callers, runtime contracts, and tests.
- Identify dead code only when there is evidence that it is unreachable or unused.
- Do not recommend a framework migration merely because another architecture is cleaner.
- Preserve working behavior as the primary constraint.

For common Lovable project shapes and boundaries, read [references/lovable-projects.md](references/lovable-projects.md).

## Phase 2: Architecture map and plan

Create a compact architecture map before recommending structural changes. Include only what is relevant:

- app entry and routing
- feature/module boundaries
- shared components and utilities
- state management
- API/data-access layer
- Supabase or other backend integrations
- auth/authorization boundaries
- server/edge functions
- external services
- tests and build tooling

Classify proposed work as:

- **Critical** — current behavior, security, data integrity, or deployability is at material risk.
- **High** — architecture or coupling is likely to cause defects or make important changes unsafe.
- **Medium** — meaningful maintainability, duplication, complexity, or performance debt.
- **Low** — cleanup with limited operational benefit.

Use [references/report-format.md](references/report-format.md) for the audit output.

At the end of the audit, stop and request explicit approval for the first proposed batch.

## Phase 3: Safe refactor execution

After explicit approval, read [references/refactor-playbook.md](references/refactor-playbook.md).

Apply the smallest coherent change that improves the approved issue while preserving public behavior.

For every batch:

1. State the exact goal and files/surfaces expected to change.
2. Identify the behavior/contracts that must remain unchanged.
3. Make the smallest viable refactor.
4. Remove only dead code made obsolete by the approved change or proven unused code included in scope.
5. Run or inspect the strongest available verification.
6. Compare observed behavior/contracts with the pre-refactor baseline.
7. Report what changed, what was verified, and any residual risk.
8. Stop if verification fails or unexpected coupling appears; investigate before continuing.

Do not combine unrelated cleanup into the same batch.

## Protected boundaries

Treat the following as protected unless the user explicitly approves the specific change:

- database schema and migrations
- RLS policies and grants
- authentication/session behavior
- authorization/role logic
- production data transformations or deletions
- public routes and URLs
- API request/response contracts
- external integration contracts and webhooks
- environment/secrets configuration
- billing/payment flows
- analytics/event names relied on externally

For Supabase-specific rules, read [references/supabase-guardrails.md](references/supabase-guardrails.md).

If a dedicated Supabase skill is available, use it for Supabase-specific schema, RLS, Auth, SQL, migration, index, or database-performance work. This skill remains responsible for the refactor sequence and approval gates.

## Refactoring principles

Prefer these transformations when evidence supports them:

- split components by responsibility, not arbitrary line count
- move reusable business logic out of presentation components
- centralize repeated integration/data-access code when semantics truly match
- replace duplicated literals with shared constants only when they represent the same concept
- reduce prop drilling when it creates real coupling; do not add global state by default
- keep feature-specific code near the feature unless sharing is proven
- make types stricter at boundaries without broad unsafe rewrites
- simplify conditionals and data transformations while preserving edge cases
- remove unnecessary wrappers and premature abstractions
- keep naming aligned with the business concept represented in the code
- prefer local, incremental architecture improvement over repository-wide redesign

Do not optimize for fewer files, more files, a specific folder pattern, or a fashionable architecture. Optimize for clarity, cohesion, safe change, and verifiable behavior.

## Verification

Read [references/verification.md](references/verification.md).

Use the best available evidence in this order when applicable:

1. existing automated tests
2. type checking / static analysis
3. linting
4. production build
5. focused manual behavior checks
6. targeted comparison of routes, API contracts, and data behavior

Never claim "no behavior change" unless it was meaningfully verified. State verification gaps explicitly.

## Interaction with code review

If a production code review report already exists, use it as audit input rather than repeating the entire review. Validate any finding that will drive a refactor before changing code.

If no review exists, perform the audit in this skill first. The purpose here is not to produce the broadest possible review; it is to find and safely execute high-value refactors.

## Completion criteria

Consider a refactor batch complete only when:

- the approved issue was addressed
- protected contracts were preserved or separately approved
- available verification passes
- no unexplained regression remains
- the change is smaller and easier to reason about than the state it replaced
- the report records verification and residual risk

After a major sequence of batches, recommend a fresh production code review before release.
