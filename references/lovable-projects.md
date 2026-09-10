# Lovable Project Guidance

Treat the repository as the source of truth. Lovable projects can evolve substantially after initial generation, so do not assume a fixed folder layout or framework version.

## Inspect before refactoring

Check the actual project for:

- package manager and scripts
- build tool and framework configuration
- routing setup
- TypeScript configuration
- component/library conventions already in use
- state management and query/cache libraries
- backend or Supabase integration code
- edge/server functions
- migrations
- environment-variable access
- test tooling

Common Lovable-generated web projects may contain React/TypeScript and a Supabase integration, but activate those assumptions only when the repository confirms them.

## Preserve the product surface

Legacy prompt-built projects often contain behavior that is undocumented but relied on by users. Preserve:

- visual behavior unless UI changes are approved
- route paths and deep links
- form field semantics and validation behavior
- query parameters
- storage keys
- API payloads
- database column semantics
- auth flows
- role-based visibility
- analytics identifiers
- external callbacks and webhooks

## Improve architecture incrementally

Prefer a feature-oriented structure when it matches existing product boundaries, but do not force a repository-wide folder migration.

Typical safe moves include:

- extract pure utilities from oversized components
- extract cohesive hooks around reusable UI/business behavior
- isolate API/data access from rendering code
- consolidate duplicate request/error mapping
- create shared UI only for truly shared presentation patterns
- define boundary types near APIs/integrations
- move feature-specific helpers closer to their feature

Avoid "cleanup" that changes every import path in the repository without a functional reason.

## Lovable editing behavior

When working inside Lovable, keep batches small enough that the generated change can be reviewed in the editor before proceeding. If the platform exposes a diff/history/checkpoint, use it to make rollback easy. Do not assume an unavailable tool exists; report the rollback method actually available in the project/session.
