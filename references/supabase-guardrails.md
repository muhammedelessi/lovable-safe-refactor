# Supabase Guardrails

Treat Supabase as a protected boundary during refactoring.

## Do not change without explicit approval

- tables, columns, constraints, or relationships
- migration history
- RLS enablement or policies
- grants/roles
- auth/session behavior
- storage policies
- database functions/triggers
- Edge Function externally observable contracts
- production data
- secrets or service-role usage

## Safe refactor behavior

You may reorganize application-side Supabase access code only when query semantics, auth context, expected rows, error behavior, and returned shapes remain equivalent and are verified.

Before centralizing two Supabase queries, confirm they truly use the same filters, ordering, joins, authorization assumptions, null behavior, and error semantics.

Do not "fix" RLS by bypassing it, moving privileged keys to the client, or adding service-role access. Never expose service-role or secret keys in browser code.

If a refactor exposes a probable Supabase security or schema defect, report it separately. Do not change the protected boundary until the user explicitly approves that specific fix.

If a dedicated Supabase skill is available, use it for detailed Supabase/SQL/RLS/Auth work and keep this skill's approval/batching workflow around the change.
