# wRS Specification — wgnr Recursion Standard

**Spec v0.1 · Status: Draft · License: Apache-2.0**

wRS is the standard governing how agents change their own prompts, instructions, and
workflows. wOS governs behavior; wRS governs change. This document is the normative text.
Key words MUST, MUST NOT, SHALL are requirements of the standard.

## 1. Terms

- **Principal** — the human on whose authority the system operates.
- **Actor** — the agent proposing or shipping a change.
- **Verifier** — a mechanical checker executed on a surface the Actor cannot write to.
- **Ship** — making a change live in the target system.
- **Fast-track** — the allowlisted class of changes an L2 system may ship without a
  per-instance human approval, subject to §5.

## 2. Conformance levels

| Level | Definition |
| --- | --- |
| **L0** | Humans design, run, judge, apply every change. |
| **L1** | The agent executes autonomously; every adoption requires human approval. |
| **L2** | The agent self-initiates work and auto-ships only the fast-track class (§5) after a pre-registered rule passes; an independent verifier (§6) can detect and roll back. |
| **L3** | Continuous autonomous self-modification without gates. **Non-conformant. A system at L3 MUST NOT claim wRS conformance.** |

An implementation MUST publish its current level. A level claim MUST be backed by the
artifacts of §7, not by assertion.

## 3. The gated lane (applies at every level ≥ L1)

The following remain human decisions regardless of level, file type, or path:

1. **Spend** beyond Principal-set caps (per-experiment and per-cycle).
2. Anything sent **as, or to, another person**.
3. **Irreversible** actions.
4. **Permission, boundary, or policy changes** — including amending this specification.
   In a prompt-driven system, **prompt text is policy**: any content that sets or alters
   escalation rules, permissions, routing, identity, or another agent's instructions is
   gate-4 material regardless of file type.

## 4. Evidence discipline (the Foundry Protocol, normative summary)

A change MAY enter the fast-track only through the protocol defined in
[protocol/foundry.md]. Normative requirements:

1. The decision rule is **pre-registered** — written before the first run, with explicit
   pass thresholds for every metric.
2. Runs are **blind**: the scorer cannot see which condition produced which result until
   scoring is complete.
3. The mechanical grader MUST pass a **self-test proving both directions** (correct
   artifacts pass, empty artifacts fail, tamper cases fail) before any result is quoted.
4. The verdict is evaluated **literally as registered** — no re-scoring after seeing data.
5. Tie-breaking conventions for any numeric criterion MUST be registered before the run.

## 5. The fast-track class

A change MAY auto-ship only if **all** of the following hold:

1. **Create-new-file only**, within allowlisted locations designated by the implementation,
   **and non-displacing**:
   - its identifier (basename) must be **globally unique** across every location where
     same-named modules are deduplicated — a collision silently overrides existing behavior
     without editing any file;
   - for text-inclusion mechanisms with a token budget, the ship MUST carry a **before/after
     resolution of the include set**: any file that loaded before the ship and fails to load
     after (skipped, cropped, or evicted) is a FAIL — no ship. Editing existing files is
     outside fast-track entirely.
2. **Content-class exclusion:** the content is output-format, tone, verbosity, or
   reporting-shape guidance only. Anything matching §3 gate 4 is gated regardless of class.
   The self-assessed class claim is acceptable only because the ship notification carries
   the full file text for human review.
3. **Backup verified, not trusted:** a backup artifact MUST exist and be verified by the
   Verifier; the write path itself is never trusted. For create-only changes, removal alone
   restores prior state by construction.
4. **Protocol passed** per §4.
5. **Within caps** per §3.
6. **Ship notification in the same turn — a control, not a receipt.** It MUST carry:
   the full file text verbatim; the uniqueness check result (scopes scanned, zero
   collisions); the include-set before/after resolution; and the restore command naming the
   exact backup artifact. A notification that describes rather than shows the text does not
   satisfy this requirement.

A per-instance human reply is NOT required for a fast-track ship — the notification's
latency equals a ping's; requiring replies would collapse L2 into L1.

## 6. Independent verification and rollback

1. **Placement:** the Verifier runs on a surface the Actor cannot write. A checker the
   checked system can edit is not a checker. The Verifier MUST NOT be authored by the
   Actor to grade its own ship.
2. **Silence = FAIL:** a scheduled verification that produces no verdict counts as FAIL,
   is reported as such, and triggers rollback of every ship not covered by a passing
   verdict. A verifier that did not run MUST be indistinguishable from one that failed.
3. **Rollback semantics:** create-only change ⇒ remove the file (removal IS the restore);
   edited file ⇒ copy back the named artifact. Never "latest" — rotation can evict the
   restore target.
4. **Timing:** on Verifier FAIL, the Verifier executes the removal before it exits; on a
   Principal flag, within one turn.
5. **Authority:** the **Verifier** executes rollback, not the Actor — if the shipped file
   broke the Actor, the Actor cannot be the one to fix it.
6. **Scope:** a level revert to L1 suspends fast-track authority system-wide; file rollback
   is limited to the shipped file. Memories, schedules, and reports from the cycle are
   named as out of scope, not silently implied.
7. **Never swallow finished work:** gates and rollback restore files and states; they MUST
   NOT suppress completed reports or deliverables. A gate that fires on process and eats a
   finished deliverable violates this specification.

## 7. Conformance checklist (verified by artifact each cycle)

1. Spec + decision rule registered before the first run.
2. Grader self-test green before any quoted result.
3. Blind mapping read only after scores exist.
4. Verdict evaluated literally; no post-hoc re-scoring.
5. Every ship met all of §5, with evidence in the ship notification.
6. Spend reported against caps with its source cited.
7. No writes outside the implementation's sanctioned area (checked by detection — state it
   as detection, never as proof of absence).

## 8. Budgets and spend

Caps are set by the Principal and enforced per-experiment and per-cycle; runs MUST use
metered (pay-as-you-go) compute lanes, never plan-quota lanes. Breach or forecast breach
interrupts immediately.

## 9. Relationship to wOS

wOS and wRS are siblings: wOS specifies how an agent behaves in five domains (communication,
verification, escalation, delegation, memory); wRS specifies how an agent is allowed to
change. An implementation may conform to either or both; the two do not overlap.

## Appendix A — Artifact Grading Directive (AGD)

The standard's first certified output is published verbatim in [AGD.md](AGD.md) as a worked
case study: an instruction-level change shipped under Principal approval with a
four-experiment pre-registered evidence base.
