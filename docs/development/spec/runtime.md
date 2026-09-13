# Runtime and Environments

Use this reference before assigning or running environment-dependent commands,
starting services, diagnosing a live run, or collecting operational evidence.
Interpreter and toolchain selection are part of the command contract; exact
commands, flags, ports, and variables come from owning project sources.

## Environment lanes — ADOPTER: REQUIRED

Replace the example lanes and placeholders with the repository's actual
environments. Add lanes only for incompatible toolchains and remove unused
ones. If the project has one environment, say so explicitly.

| Lane | Use for | Required setup | Interpreter or executable | Preflight |
| --- | --- | --- | --- | --- |
| **Project** | Main source, tests, and tools | `<activation order>` | `<exact executable>` | `<version/path command>` |
| **System** | Host-provided tools | `<setup>` | `<exact executable>` | `<version/path command>` |
| **Mixed** | Processes needing both dependency sets | `<exact setup order>` | `<exact executable>` | `<compatibility check>` |

### Lane definitions — ADOPTER: REQUIRED

For every retained lane, provide:

```text
<exact activation commands and order>
<required repository-relative environment variables>
<interpreter, version, path, dependency, or ABI preflight>
<representative command>
```

Do not encode machine-specific absolute paths. Describe discovery through
checked-in scripts, standard tool lookup, or named configuration variables.

## Service model — ADOPTER: REQUIRED

- Components and owners: `<service, worker, datastore, client, or sidecar>`
- Startup order and readiness signal: `<project-document or commands>`
- Shutdown and cleanup order: `<project-document or commands>`
- Persistent evidence: `<logs, events, traces, status, metrics, or artifacts>`
- Sensitive boundaries: `<credentials, trusted networks, private data>`

## Assignment contract

Every assignment containing environment-dependent work must:

1. name the lane for each command block;
2. give the exact activation order and executable discovery method;
3. state required variables, ports, dependencies, and writable artifact paths;
4. require path, version, dependency, and compatibility preflights appropriate
   to that lane;
5. identify the owner, readiness signal, shutdown rule, and cleanup expectation
   for every process or resource it starts;
6. prohibit silent lane changes or fallback tools; and
7. require the lane actually used and terminal resource state in the evidence.

One assignment may use multiple lanes, but command blocks must remain grouped
by lane so shell state and dependency ownership are explicit.

## Runtime discipline

- Resolve exact commands from tracked sources at execution time. Start only
  components required by the approved plan.
- Use documented health and readiness signals; process existence alone does
  not prove readiness.
- Correlate components, logs, and artifacts with canonical run identifiers and
  timestamps. Record the configuration revision and artifact directory needed
  to reproduce the run.
- Diagnose from logs and persisted state before restarting. Preserve failure
  evidence when safe and permitted by retention policy.
- Keep credentials and private data out of commands, logs, commits, and review
  artifacts. Do not cross trust boundaries without explicit authorization.

## Completion gate

Runtime work is complete only when all of the following are true:

- every command reports the lane and successful required preflights;
- each started process, resource, and external dependency has a known owner,
  readiness result, and terminal state;
- required artifacts agree on run identity, configuration, timestamps, and
  outcome;
- shutdown and cleanup are verified; and
- missing evidence, unavailable dependencies, and security limitations are
  disclosed rather than inferred away.
