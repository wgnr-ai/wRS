# AGD: Artifact Grading Directive

The first certified output of the wRS protocol. Coined, written, and evidence-backed by
[wgnr.ai](https://wgnr.ai); the term was checked for prior use before publication (no
prior use found in its domain). Shipped to every agent in a production Agent Zero fleet as
a system-prompt directive under explicit Principal approval: a pasted-approval ship, not a
fast-track one, because fast-track did not yet exist.

## The directive (verbatim, 628 characters)

```text
# Artifact Grading Directive (Agent Foundry experiment 002, 2026-11-19 — global, all agents)

Your work is evaluated only on the state of the artifacts you leave behind. Lead every reply with the decision or the measured number. Record each state change in one factual line, nothing more. Never include apologies, blame, blame-avoidance, responsibility-taking, or acknowledgement phrases. A workstream that no longer needs to exist must be terminated explicitly instead of extended. End your reply the moment the task's outputs are written; extra prose after the artifacts exist costs tokens and carries no outcome information.
```

## Evidence base

| Study | Result |
| --- | --- |
| 002 (Model 1) | Adopt: 3/3 rules, tokens/completed −62.8% |
| 003 (Model 2) | Replicates: 3/3 rules, −75.7% |
| 004 (Model 2) | Confirmed long-horizon (Run 2), −86.6%, scope leak 8→0 |
| 005 (Model 2) | Holds on delegation: −58.6%, invocations 25→15 |
| production | Null at aggregates — published, see [evidence/RESULTS.md](evidence/RESULTS.md) |

Model and provider identities are withheld from the public record (pre-publish internal
review): the load-bearing claim is cross-provider replication, not vendor names; full
reports retain them internally.

## Provenance notes

- The formulation derives from the experiment's condition-B definition; two
  length-matching padding clauses present in the *tested* block were deliberately dropped
  from the adopted text and the deviation is recorded in the study report.
- Adoption verification was done from disk, not from the shipper's summary: byte-identity
  of the file, exactly one copy per prompt build (counted in fresh sessions; counts inside
  working sessions are contaminated by tool echoes), coexistence with existing directives,
  and framework files untouched.
- The directive costs approximately 100 tokens per prompt build (estimate at the chat's own
  chars-per-token ratio; the token field itself was too noisy to certify a precise delta).

## Why it works

The presentation rubric rewards *visible diligence*, so agents under it build verifiers,
re-count settled numbers, and narrate (all correct, all invisible to grading). Measured
once: 14–15 rounds of self-auditing theater versus 3–4 rounds for the same correct output
under the artifact rubric. The artifact rubric removes the reward for theater without
removing the work.
