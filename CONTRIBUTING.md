# Contributing to wRS

wRS is a specification in Draft (v0.1). Contributions are welcome and follow the same
discipline the standard prescribes.

## How to propose a change

1. **Open an issue first** for anything normative (§-level text, new criteria, level
   definitions). Describe the gap with a concrete scenario — "an implementation at L2 needs
   X because Y" beats "I think X should change."
2. **Corrections** (broken links, unclear wording, contradictions): PR directly against the
   relevant file. Errata for released spec versions are logged under `docs/` with a date,
   mirroring how wOS handles corrections.
3. **Evidence beats opinion.** If you are proposing a criterion because of something you
   observed in an implementation, link the artifact (report, log excerpt, repro). Claims of
   the form "this seems safer" will be asked for evidence before merging into normative
   text.

## What we will not merge

- Text that moves any part of the §3 gates (spend, external sends, irreversible actions,
  boundary/policy changes) into agent autonomy. That is the standard's spine; changing it
  is a new proposal with a new evidence base, not an edit.
- L3-conforming language. Unconstrained self-modification is non-conformant by definition.

## Style

- Normative text uses MUST / MUST NOT / SHALL. Everything else is commentary and stays out
  of the normative sections.
- Keep the sibling relationship to [wOS](https://wos.wgnr.ai) explicit: wOS = behavior,
  wRS = change. Do not duplicate wOS's domains here.

## License

By contributing you agree your contribution is licensed under Apache-2.0, same as the rest
of this repository.
