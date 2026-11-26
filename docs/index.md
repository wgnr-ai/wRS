# wRS corrections and errata

## 2026-11-26: pre-release note (spec v0.1 Draft)

Draft assembled from a production governance rollout that ran three independent review
rounds before adoption. Known open items at v0.1:

- The include-set resolution requirement (§5.1) assumes a text-inclusion mechanism that
  reports per-file load status. Implementations without such a mechanism MUST provide an
  equivalent before/after load report or treat §5.1 as unsatisfiable (i.e., no fast-track
  for text-inclusion paths).
- Verifier placement (§6.1) is stated as a property ("a surface the Actor cannot write"),
  not a prescribed host. Reference implementations we have seen place it outside every
  container mount of the target system.
- Spend measurement (§7.6) intentionally does not prescribe a ledger format; only that the
  number carries its source.

## Publication-gate record

- **wOS upstream facts re-verified 2026-11-26** against `wgnr-ai/wOS` SPECIFICATION.md @
  commit `4c0e2d859b7d` (2026-11-24): domain sections 3.1–3.7: communication,
  verification, escalation, identity, delegation, memory, lifecycle (seven); the wOS landing
  page frames these as five core behavior domains. Because our text initially cited the
  landing's five-domain framing, SPEC §9 was rewritten count-free and now defers to upstream.
  Links (`wos.wgnr.ai`, `github.com/wgnr-ai/wOS`) confirmed live.
- **Pre-publish exclusion additions applied (independent internal review, 2026-11-26):**
  model/provider identities stripped, 5 occurrences across evidence + case study;
  delegation-gate incident references confirmed absent by grep (the normative "never swallow
  finished work" principle in §6.7 is retained as methodology and references no incident);
  backup artifact naming patterns, secret-store key names, and internal project slugs
  confirmed absent by grep.
