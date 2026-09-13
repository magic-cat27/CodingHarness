# Quality

Use this reference to select proportionate verification and to review code,
tests, runtime claims, artifacts, or a proposed change. Test configuration and
documented project commands are authoritative. A handoff summary indexes
evidence; it does not replace inspection of the actual change and evidence.

## Test map — ADOPTER: REQUIRED

| Change type | Narrow check | Broader check | Required environment lane |
| --- | --- | --- | --- |
| Unit or pure logic | `<command>` | `<command>` | `<lane>` |
| Public interface or contract | `<command>` | `<command>` | `<lane>` |
| Integration or persistence | `<command>` | `<command>` | `<lane>` |
| Runtime or service lifecycle | `<command>` | `<command>` | `<lane>` |
| Documentation or configuration | `<command>` | `<command>` | `<lane>` |

## Project invariants — ADOPTER: REQUIRED

- `<Invariant that must remain true across implementations.>`
- `<Public compatibility or data-boundary invariant.>`
- `<Lifecycle, cleanup, observability, or security invariant.>`

## Verification selection and failure paths

- Put regressions beside the behavior they protect and name tests for
  observable outcomes.
- Use the smallest check that can credibly prove the acceptance claim. Use
  integration or live evidence when mocks cannot establish it, and state all
  required dependencies.
- Cover the successful transition and relevant rejection, failure, timeout,
  cleanup, compatibility, and recovery transitions.
- Verify schemas and persistent artifacts at stable boundaries. Run broader
  regression when a change crosses shared interfaces or the narrow check
  cannot expose likely collateral failures.
- Never weaken an assertion or delete a failing test solely to make a change
  appear complete.

## Evidence rules

- Record the exact command, environment lane, result, and relevant artifact.
- Confirm that skips, mocks, caches, or unavailable services did not substitute
  for the claimed behavior. A skipped or unavailable check is a disclosed
  limitation, not a pass.
- Treat generated evidence as a set: identities, timestamps, terminal state,
  and summaries must agree across related files and views.
- Inspect representative output for user interface, logging, monitoring,
  media, or replay changes. A process exit code or dashboard alone may not
  establish the acceptance claim.

## Review order

1. Resolve approved scope and fixed decisions. Account for every changed path
   and flag work outside the assigned ownership boundary.
2. Trace each behavior change through its public interface, state transitions,
   error and cleanup paths, tests, and user-facing documentation.
3. Reproduce the claim with the narrowest credible check and inspect persisted
   evidence for internal agreement.
4. Examine likely regression surfaces and applicable compatibility, security,
   privacy, concurrency, data-loss, and rollback implications.
5. Classify each gap as a defect, environment limitation, intentional
   non-goal, or material decision requiring Planner or user escalation.
6. Record actionable findings in `../../../docs-agent/REVIEW.md` with specific
   evidence and revision instructions.

## Completion gate

Quality review is complete only when all of the following are true:

- every changed path and acceptance condition is accounted for;
- the narrow regression passes and relevant failure paths are covered;
- persisted or runtime evidence is internally consistent where required;
- every broader check not run is named with its reason and residual risk;
- findings cite reproducible evidence and no blocking finding remains; and
- the complete dirty working tree is understood before commit authorization.
