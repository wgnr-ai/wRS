# The Foundry Protocol

The method by which a change earns its way into the fast-track class (wRS §4–§5). Named for
the workshop tradition: raw question in, tested artifact out, nothing ships on opinion.

## The shape

```
question → SPEC (rule registered) → fixtures frozen → blind runs
        → self-tested grader → literal verdict → adopt-or-reject → gated ship
```

## Steps

1. **SPEC first, runs later.** Write the hypothesis, design, and pre-registered decision
   rule with explicit pass thresholds BEFORE any run exists. The rule is what makes a
   verdict a verdict; "looks better" is not one.
2. **Freeze the fixtures.** Build task inputs and ground truth before the first run. Editing
   either afterward is the line between pre-registration and p-hacking.
3. **Length-match your treatments.** If conditions differ in instruction length, match them
   (we held ours within ±5%) and keep the adoptable core separable from matching padding.
   Apparatus that gets silently adopted is apparatus that was never tested.
4. **Blind by construction.** Run directories carry no condition labels; the condition map
   lives outside the scorer's reach and is read only after scores exist.
5. **Self-test the grader in both directions** (correct artifacts PASS, empty artifacts
   FAIL, tampered artifacts FAIL) before quoting any result. A grader that cannot fail is
   a grader that cannot grade.
6. **Register tie rules.** Any numeric criterion needs its rounding/tie convention written
   down beforehand. (Ours didn't; a mean of exactly 112.625 failed a run on banker's-vs-
   half-up rounding, a fixture defect, not an agent failure, and it survived only because
   the verdict was robust to reclassification.)
7. **Evaluate literally.** All conditions pass or none do. Report per-task, not pooled.
8. **Report what failed.** Limitations, untested hypotheses, owned defects, and null results
   go in the report. A report without a failure section is marketing.

## Pitfalls we paid for (so you don't)

- **Certificates, not networks.** Every run dying identically with TLS errors is a missing
  CA bundle, not an outage. Probe the endpoint once before building.
- **Contaminated counts.** Never count prompt strings inside a working session's log.
  Tool calls echo source files, greps, and reports. Count in fresh sessions, or cross-check
  with arithmetic you can do by hand.
- **Token fields are noisy.** The same field on the same conversation swung ±700 across
  turns in our tests. Let presence checks carry acceptance; label token deltas honestly.
- **A guard that blocks cleanup steals rounds from the condition that cleans up.** Our
  safety guard blocked `rm`; the tidy condition retried deletion and lost the rounds metric
  on exactly those tasks. Either allow cleanup in-sandbox or separate blocked retries from
  round counts before you read a termination result.
- **Empty terminal messages are a model class, not a rubric result.** A run that ends on an
  empty final message after inspection is a completion failure of record. Record it, don't
  retry it post-hoc unless an anomaly policy was pre-registered.
- **Quota lanes and automation don't mix.** Automations ride metered lanes only.
- **A completion miss caused by worker-side cap exhaustion is still a miss.** Attribute it
  in the report; never re-run it into compliance.

## What the protocol has produced

Four pre-registered experiments and one production check, all published including the null:
[evidence/RESULTS.md](../evidence/RESULTS.md).
