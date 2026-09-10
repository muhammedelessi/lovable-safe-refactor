# Verification Strategy

Verification must match the risk of the batch.

## Baseline

Before a risky refactor, determine what currently passes. Record pre-existing failures.

## Preferred checks

Use available project scripts rather than inventing commands. Inspect package scripts/configuration first.

When applicable, run or inspect:

- targeted unit/component/integration tests
- TypeScript/type analysis
- lint/static analysis
- production build
- route rendering/navigation
- critical form flows
- auth/role behavior
- API request/response compatibility
- Supabase query behavior
- edge/server function behavior

## High-risk areas

For auth, payments, permissions, persistence, destructive actions, migrations, and external integrations, require stronger evidence than a successful build.

## Verification honesty

Differentiate:

- **Verified** — directly checked with suitable evidence.
- **Partially verified** — some checks passed but important gaps remain.
- **Not verified** — no reliable check was available.

Never infer runtime correctness solely from clean TypeScript, lint, or a successful build.
