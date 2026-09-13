# Agent Router

This file is the entry point for a portable User → Planner GPT-Work →
Executor GPT-Work → Codex workflow. Copy the contents of this migration bundle
to the target repository root, then customize the sections marked
`ADOPTER: REQUIRED` before using the workflow.

## Adoption checklist

The adopter must replace or complete all of the following:

1. **Repository overview:** describe the product, its users, and its main data
   or request flow.
2. **Repository structure:** replace every `<project-path>` entry with a real
   repository-relative path, adding or removing rows as needed.
3. **Public document routing:** replace each `<project-document>` entry with an
   existing project file or remove the row when the project has no such source.
4. **Development references:** customize every `ADOPTER: REQUIRED` section in
   `docs/development/`, especially environment lanes, commands, conventions,
   invariants, and artifact limits.
5. Initialize `docs-agent/SPEC.md`, `docs-agent/PLAN.md`,
   `docs-agent/STATUS.md`, `docs-agent/REVIEW.md`, and
   `docs-agent/MEMORY.md` for the first real task. Do not leave template
   examples as verified project facts.

Paths named below are repository-relative after the bundle contents are copied
to the target repository root. A path written as `<project-path>` or
`<project-document>` is an adopter-supplied project file, not a file included
in this bundle.

## Repository overview — ADOPTER: REQUIRED

**Product:** `<describe the repository>`

**Core flow:** `<input> → <major component> → <major component> → <output>`

**Primary constraints:** `<list durable product or operational constraints>`

## Roles and authority

- **User:** has the repository's highest authority. Sets direction, states
  requirements, approves plans and acceptance criteria, controls material
  side effects, and uses the delivered product.
- **Planner GPT-Work:** turns user requirements into specifications and
  executable plans for Executor GPT-Work. Changes this document system only
  when the user requests it.
- **Executor GPT-Work:** implements an approved plan through Codex. Assigns
  bounded work, reviews actual changes and evidence, and requests revisions
  until completion criteria are satisfied.
- **Codex:** performs bounded execution. Changes only assigned paths, runs
  required checks, preserves unrelated work, and reports evidence.
- **Activation:** Planner GPT-Work is the default. Executor GPT-Work starts
  only from `Role: Executor GPT-Work`; Codex starts only from an Executor
  assignment beginning with `Role: Codex`.

The user may override any lower-level decision. A lower role must return a
material ambiguity or scope change upward instead of deciding it silently.

## File routing

### Repository structure — ADOPTER: REQUIRED

| Looking for | Path |
| --- | --- |
| `<project area or responsibility>` | `<project-path>` |

### Role routing

| Role | Role file |
| --- | --- |
| Planner GPT-Work | `docs-agent/role/Planner.md` |
| Executor GPT-Work | `docs-agent/role/Executor.md` |
| Codex | `docs-agent/role/Codex.md` |

Read the matching role file completely when that role becomes active.

### Public document routing — ADOPTER: REQUIRED

| Trigger | File |
| --- | --- |
| Implement, modify, verify, review, run, or publish project changes | `docs/development/development.md` |
| Design, restructure, or maintain AGENTS.md and its routed document system | `docs/document/document.md` |
| `<project-specific information need>` | `<project-document>` |
