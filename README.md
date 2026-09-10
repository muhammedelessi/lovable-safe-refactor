# Lovable Safe Refactor

A Lovable-specific AI agent skill for safely improving large legacy or prompt-built projects without turning cleanup into a risky rewrite.

> **Version:** 1.0.0  
> **Status:** Public / reusable  
> **License:** MIT

The skill is designed for projects that grew through repeated prompts, inconsistent implementation, duplicated logic, oversized components, fragile boundaries, or unclear architecture.

## Core workflow

**Audit -> Architecture Map -> Prioritized Plan -> Explicit Approval -> Small Refactor Batch -> Verify -> Re-review**

The initial audit is read-only. Refactoring starts only after the user explicitly approves a proposed batch.

## What it protects

By default, the skill preserves existing UI and behavior and treats the following as protected boundaries: database schema and migrations, Supabase RLS, Auth, production data, routes, API contracts, external integrations, environment/secrets configuration, payment flows, and externally relied-on analytics events.

## Import into Lovable

1. Open your Lovable workspace.
2. Go to **Settings -> Skills -> Import -> GitHub**.
3. Paste this repository URL:

```text
https://github.com/muhammedelessi/lovable-safe-refactor
```

4. Import the skill and keep it enabled on Lovable projects that need controlled cleanup or architecture improvement.

## Example requests

```text
Audit this Lovable project and create a prioritized refactoring plan. Do not modify code yet.
```

```text
Identify duplicated logic, oversized components, and weak feature boundaries in this project.
```

```text
Refactor only the first approved batch and verify behavior before continuing.
```

```text
Clean up this legacy Lovable feature without changing UI, routes, Auth, RLS, or database contracts.
```

## Intended use

Use it for Lovable projects with technical debt from prompt-driven development. It is intentionally scoped to Lovable and should complement, not replace, a broad production code review or a dedicated Supabase skill.

## Repository structure

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── audit-framework.md
│   ├── lovable-projects.md
│   ├── refactor-playbook.md
│   ├── report-format.md
│   ├── supabase-guardrails.md
│   ├── verification.md
│   └── sources.md
├── CHANGELOG.md
├── CONTRIBUTING.md
└── LICENSE
```

## Safety model

The skill favors small reversible batches, preserves working behavior as the primary constraint, stops when verification fails or unexpected coupling appears, and requires explicit approval for protected-boundary changes.

## Contributing

Issues and pull requests are welcome. See `CONTRIBUTING.md` before proposing workflow or safety changes.
