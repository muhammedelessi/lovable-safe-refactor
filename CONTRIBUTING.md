# Contributing

Thanks for helping improve this skill.

## Safety rules

- Preserve the audit-first, approval-gated workflow.
- Do not allow broad automatic rewrites of legacy Lovable projects.
- Keep protected boundaries explicit for database schema, migrations, RLS, Auth, production data, routes, APIs, integrations, secrets, payments, and externally relied-on analytics.
- Prefer small reversible batches with verification after each batch.
- Do not mix feature development with unrelated cleanup.
- Keep Lovable-specific behavior in this repository; use dedicated skills for broad code review or Supabase-specialist work.

## Pull requests

Describe the legacy-project problem being addressed, the proposed workflow change, its safety implications, and how the change was verified against realistic Lovable project scenarios.

## Versioning

Use semantic versioning. Any change that weakens approval gates, protected boundaries, or verification requirements should be treated as a breaking change.
