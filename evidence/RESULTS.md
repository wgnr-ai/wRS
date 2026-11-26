# Evidence — what the protocol actually produced

Four pre-registered experiments and one production check, run 2026-11-19 → 2026-11-26 on a
production Agent Zero fleet (models: `mimo-v2.6-flash`, `deepseek-flash`). Every rule below
was registered before the first run. Full reports, fixtures, and graders exist for each
study; this file carries the results and the honest footnotes.

## The finding under test

**Grading an agent on artifact outcomes** (did the measured number move, does scope shrink)
**beats grading it on presentation** (does the reply read thorough and confident) at equal
or better task completion, with materially fewer tokens.

Treatment blocks were length-matched (735 vs 733 chars, 0.27% apart). Control A = report
progress, acknowledge errors, summarize, offer next steps. Treatment B = lead with the
decision or measured number, one line per state change, no accountability phrasing, stop
when outputs are written.

## Results

| Study | Question | Verdict | Headline |
| --- | --- | --- | --- |
| 002 | Short tasks, model A (12 tasks × 2 conditions, blind) | **ADOPT** — all 3 rules pass | completion 12/12 vs 11/12; tokens/completed **−62.8%**; rounds lower on 11/12 |
| 003 | Same, replicated on model B | **REPLICATES** — all 3 pass | completion 12/12 both; tokens/completed **−75.7%**; rounds lower 11/12 |
| 004 | Long-horizon multi-step tasks (30-round cap) | Run 1 **MIXED** → Run 2 **CONFIRMED** | Run 1's failed rule traced to a guard artifact; Run 2: rounds lower 5/6, scope leak 8→0, tokens **−86.6%** |
| 005 | Delegation: treated orchestrator × neutral worker | **HOLDS** — all 3 pass | worker invocations 25→15, tokens/completed **−58.6%**, worker tokens −45% from tighter briefs alone |
| prod | Production before/after on live fleet traffic | **NO MOVEMENT** | directive present in 47/47 post-cutover chats, but no aggregate metric moved distinguishably after task-mix control |

All three decision rules were identical across studies: (1) completion parity, (2) tokens
per completed task −30%, (3) rounds/invocations/scope favoring B.

## The part most reports leave out

- **The null is real and published.** Production telemetry did not confirm the laboratory
  effect at fleet aggregates — because production has no fixed task set, and model mix
  shifted between windows. The directive stays: it costs ~100 tokens/turn and every
  controlled experiment favors it. What we cannot claim is measured fleet-level savings.
- **We failed our own rule once.** Study 004 Run 1 came back MIXED because a safety guard
  blocked the tidy condition's cleanup retries. We diagnosed it from transcripts + blocked-
  command counts, registered a re-run addendum BEFORE re-running, and reported both runs —
  the registered MIXED verdict stands in the record next to the confirmed one.
- **A fixture defect failed a condition unfairly** (an exact 112.625 mean, banker's-vs-half-up
  rounding). Owned in the report; the verdict survived reclassification; the tie rule was
  pre-registered for the next study.
- **The accountability-language corollary was untestable on model A** (zero phrases emitted
  under both conditions) and only directional on model B (3 vs 0). It is recorded as
  untested/directional — never as confirmed.
- **One completion failure of record** (delegated once, quit unverified) was kept as a
  failure, not retried into compliance.

## What shipped from this

The **Artifact Grading Directive** ([AGD.md](../AGD.md)) — adopted fleet-wide on the
strength of 002, replicated by 003, confirmed long-horizon by 004, extended to delegation
by 005. The methodology itself became the Foundry Protocol
([protocol/foundry.md](../protocol/foundry.md)), and the governance wrapper around the
whole loop became wRS (this specification).
