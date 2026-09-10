# Lovable Safe Refactor

A Lovable-specific agent skill for improving large legacy or prompt-built projects without turning cleanup into a risky rewrite.

## Workflow

**Audit -> Architecture Map -> Prioritized Plan -> Explicit Approval -> Small Refactor Batch -> Verify -> Re-review**

The initial audit is read-only. The skill does not begin refactoring until the user explicitly approves the proposed batch.

## Key protections

It preserves existing UI and behavior by default and treats database schema, migrations, Supabase RLS, Auth, production data, routes, API contracts, external integrations, secrets, payments, and analytics contracts as protected boundaries that require explicit approval to change.

## Intended use

Use it for Lovable projects that have accumulated duplicated code, oversized components, mixed responsibilities, inconsistent data access, fragile architecture, weak boundaries, or technical debt from prompt-driven development.

It is intentionally scoped to Lovable projects. For general code-quality review, use a separate production code review skill. For Supabase-specific schema/RLS/Auth/SQL work, use an official or dedicated Supabase skill.
