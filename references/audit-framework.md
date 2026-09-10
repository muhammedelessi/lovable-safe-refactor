# Audit Framework

Use this framework before changing a legacy Lovable project.

## 1. Establish scope

Determine whether the request targets the whole project, one feature, one route, one integration, or one known pain point. For very large projects, sample architecture broadly first, then deep-dive into the highest-risk areas instead of reading every file mechanically.

## 2. Build a dependency picture

Identify entry points, routes, feature boundaries, shared modules, state/data flows, API clients, auth, database access, edge/server functions, environment configuration, and tests.

Trace both directions around risky code:

- who calls it?
- what does it call?
- what contract does it expose?
- what assumptions do consumers make?
- what persistent data or external systems does it touch?

## 3. Detect high-value technical debt

Look for evidence of:

- oversized components with mixed responsibilities
- duplicated business rules or data-access logic
- repeated API/Supabase calls implemented inconsistently
- UI components containing authorization or persistence logic
- circular or tangled dependencies
- feature code depending on unrelated feature internals
- inconsistent error/loading/empty-state handling
- unsafe or weak typing at trust boundaries
- stale wrappers and abandoned abstractions
- hard-coded business values repeated across the codebase
- unnecessary global state
- state duplicated between local, URL, cache, and backend sources
- effects that synchronize state unnecessarily or hide business logic
- async race conditions or missing cleanup
- unreachable or proven-unused code
- configuration/secrets embedded in source
- fragile route/API/database contracts with no tests
- large modules where small changes have large blast radius

## 4. Avoid false positives

Do not flag code merely because it differs from personal style. A finding should have at least one concrete consequence: defect risk, security risk, data-integrity risk, excessive coupling, repeated change cost, testability problem, performance impact, or significant cognitive load.

Do not propose abstraction until at least two real call sites have semantically equivalent behavior, unless a hard boundary (security, API, persistence) clearly warrants separation.

## 5. Rank by expected value

Prioritize work that reduces risk and makes future changes safer. Cosmetic uniformity comes last.

For each finding record:

- evidence/location
- why it matters
- likely blast radius
- recommended direction
- expected behavior to preserve
- verification needed
- whether explicit protected-boundary approval is required
