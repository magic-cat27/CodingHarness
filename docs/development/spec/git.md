# Git Workflow

Use this reference when preparing a local commit, pushing a branch, or
reviewing repository state. The user owns remote publication; Executor GPT-Work
owns implementation review and local commit authorization; Codex performs only
the authorized Git action.

## Repository policy — ADOPTER: REQUIRED

- Commit style: `<project convention>`
- Branch naming: `<project convention>`
- Protected/shared branches: `<branch names>`
- Pull-request requirements: `<project-document or policy>`
- Artifact size and tracking rules: `<limits and artifact-store location>`

## Local commit gate

1. Codex completes and verifies a logical change set, then reports its paths
   and the full remaining dirty state to Executor.
2. Executor reviews the actual diff and explicitly authorizes a commit by
   naming exact paths or logical set, required message, and exclusions.
3. Codex stages only authorized paths using explicit path staging; never use a
   repository-wide catch-all stage command.
4. Codex creates only the authorized local commit. Separate logical commits
   require separately authorized boundaries and messages.
5. Executor verifies commit contents and accounts for every remaining staged,
   modified, and untracked path.

No review result or task completion implicitly grants commit authority. Keep
independently reversible changes separate and do not mix unrelated user work.

## Remote gate

Every push requires fresh user approval naming the exact remote and branch,
even when an upstream exists. Push only the approved ref after Executor has
verified the local commit. Never force-push, publish directly to a protected
shared branch, create a pull request, release, or deploy unless the user
explicitly authorizes that specific action.

## Artifact boundary

Track source, frozen configuration, lightweight manifests, summaries, and
indexes needed for reproducibility. Keep secrets and machine-local state out of
Git. Apply the adopter-defined artifact size and storage policy before staging
generated logs, media, databases, traces, or large data files.

Git work is complete when the authorized commit matches its exact path set and
message, remaining dirty state is documented, and no remote state changed
without the user's exact approval.

