# wRS corrections and errata

## 2026-11-26 — pre-release note (spec v0.1 Draft)

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
