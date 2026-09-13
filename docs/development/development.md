# Development

This file is the gateway for implementing, verifying, reviewing, running, or
publishing project changes. Read this baseline first, then follow only the
triggered detail routes below. Project configuration and owning public
documents remain authoritative for versioned values and exact commands.

## Project conventions — ADOPTER: REQUIRED

- Source roots: `<repository-relative paths>`
- Test roots: `<repository-relative paths>`
- Formatter, linter, and type checker: `<tools and owning config files>`
- Naming and language conventions: `<project rules or contribution document>`
- Generated files: `<locations and regeneration commands>`
- Public behavior sources: `<project-document paths>`
- Compatibility, security, privacy, and data invariants:
  `<owning documents or concise invariant list>`

## Common change discipline

- Inspect nearby implementation, configuration, tests, and working-tree state
  before editing. Reuse existing interfaces and ownership seams when they
  satisfy the approved behavior.
- Make the smallest coherent change that satisfies the approved specification.
  Preserve unrelated changes and avoid broad rewrites whose full output is not
  assigned and reviewable.
- Keep core behavior independent from a particular client, transport, or
  deployment unless the approved specification requires the coupling.
- Use repository-relative paths in tracked configuration and runtime logic
  unless a documented portability mechanism requires a named variable.
- Name code and tests for enduring observable behavior. Comment live
  constraints and non-obvious reasoning rather than restating the code.
- Update the owning user or design document when its public contract changes.
  Treat dependencies, schemas, migrations, generated code, and public APIs as
  explicit plan items with compatibility and recovery evidence.
- A change is not complete merely because code was edited or one check passed.
  Apply every detail route triggered by the work and satisfy its completion
  gate.

## Detail routing

| Trigger | Read |
| --- | --- |
| Select tests, assess failure paths, review a change, validate evidence, or decide whether implementation is complete | `spec/quality.md` |
| Select an interpreter or toolchain, start or diagnose a service, manage a live run, or collect operational evidence | `spec/runtime.md` |
| Inspect repository state for a commit, prepare or create a local commit, push, open a pull request, release, or deploy | `spec/git.md` |
