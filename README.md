# wRS

### The open self-improvement governance standard for AI agents.

[Read the Spec](SPECIFICATION.md) · [The Protocol](protocol/foundry.md) · [Evidence](evidence/RESULTS.md) · [Case Study: AGD](AGD.md) · [Contribute](CONTRIBUTING.md)

![License](https://img.shields.io/badge/license-Apache--2.0-blue)
![Spec Version](https://img.shields.io/badge/spec-v0.1-orange)
![Status](https://img.shields.io/badge/status-Draft-yellow)

## What it is

wRS governs how agents **change**: their own prompts, instructions, and workflows. wOS
governs how agents *behave*; wRS governs how they *improve*. Like wOS, it is a
specification, not a framework: it sits on top of your runtime and defines the contract a
self-improving system must satisfy before it is allowed to ship a change to itself.

The contract in one line: **improvement is earned by pre-registered evidence, shipped
through a narrow class, verified by a checker the actor cannot write, and reversible by a
party other than the one that shipped.**

## Why it exists

Agents today improve in exactly two ways, and both are wrong:

- **Ungoverned:** self-rewriting loops that edit their own instructions continuously and keep
  whatever scores better (no gates, no audit, frequently executing generated code with
  production permissions). Fast, unauditable, and one drift event from silent failure.
- **Not at all:** frozen prompts. Every improvement requires a human to notice, design,
  test, and apply it by hand. Safe, slow, and it never compounds.

wRS defines the middle path (a **charter-gated improvement loop**): an agent may
self-initiate and auto-ship inside a pre-registered, mechanically verified class, while
spend, external effects, irreversible actions, and boundary changes stay human. The level
you operate at is explicit, printed, and checkable.

## The doctrine is production-tested

wRS was authored inside [wgnr.ai](https://wgnr.ai) and validated the way it prescribes:
pre-registered decision rules, blind runs, self-tested mechanical graders, and literal
verdicts across four experiments, **including a published null result** where fleet
telemetry did *not* confirm the laboratory finding. The full evidence, including what
failed, is in [evidence/RESULTS.md](evidence/RESULTS.md).

## Conformance levels

| Level | Definition | Who it is for |
| --- | --- | --- |
| **L0** Manual | Humans design, run, judge, apply everything. | Starting out |
| **L1** Autonomous execution | The agent does the work; a human approves every change. | Most production teams today |
| **L2** Charter-gated autonomy | The agent self-initiates and auto-ships inside an allowlisted, mechanically verified class; spend, gates, and boundaries stay human; an independent verifier can roll back. | Teams with evidence discipline |
| **L3** Unconstrained self-modification | Continuous autonomous rewriting with no gates. | **Non-conformant by definition. Never.** |

## Positioning

wRS does not compete with adjacent standards. Each governs a different layer of the same
stack:

| Standard | What it governs | Relationship |
| --- | --- | --- |
| [wOS](https://wos.wgnr.ai) (wgnr.ai) | How agents behave | Sibling — behavior vs. change |
| [ACS](https://github.com/microsoft/agent-governance-toolkit) (Microsoft) | Security policy | Complementary — policy vs. change process |
| [AGENTS.md](https://agents.md/) (AAIF) | Context and instructions | Complementary — knowledge vs. change governance |
| [Agent OS](https://buildermethods.com/agent-os) (Builder Methods) | Coding standards | Complementary — code vs. self-change |
| Autonomous self-rewriting (RRSI-style) | Continuous self-modification | wRS is the gated form of exactly this; L3 marks the ungoverned form non-conformance |

## License

Apache-2.0. See <LICENSE>.

## Contributing

See <CONTRIBUTING.md>.

Built by [wgnr.ai](https://wgnr.ai) (wRS v0.1). Agents that change, proven.
