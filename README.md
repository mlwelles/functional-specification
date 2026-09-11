# functional-specification

An auto-invoked agent skill for writing functional specifications — documents stating what a system must observably do, precisely enough that an engineer can build it, QA can test it, and a stakeholder can accept or reject the result.

## What it does

The skill triggers when an agent writes, structures, or reviews a functional specification. It supplies:

- **a requirement contract** — every requirement carries a stable ID, a provenance marker, one testable statement, and criteria that trace back to it,
- **a scope test** — could two different implementations both satisfy this sentence? If not, it belongs in the design doc,
- **a fixed document shape** — nine sections in a set order,
- **fill-in templates** (full and minimal) and a pre-share checklist.

## Why the provenance marker

Specs get written from thin briefs, which forces the author to invent. Invention is unavoidable; disguising it is the defect. Every requirement is marked `[brief]`, `[decided: who, when]`, or `[assumed]`, at the point of use rather than in a prefatory section a reader never revisits.

When `[assumed]` requirements outnumber sourced ones, the skill stops the agent and sends the open questions out as a list instead of circulating a specification built on guesses.

## How it was built

Written test-first, following [superpowers `writing-skills`](https://github.com/obra/superpowers). Three agents wrote a functional specification from the same brief without the skill, establishing a baseline; their documents shared four defects:

1. acceptance criteria that cited no requirement, so nothing traced,
2. invented values stated in the same authoritative voice as sourced ones,
3. schemas, endpoints, and status codes occupying a document that should stay solution-agnostic,
4. no two documents sharing a structure.

The skill addresses those four specifically. Re-running the scenario with it produced zero orphan criteria, zero unmarked requirements, zero solution leakage, and an identical section structure across all three runs. A further round closed a defect the skill itself introduced: agents dutifully producing 4,800-word specifications from a three-sentence brief, rather than stopping to ask.

Per `writing-skills`, the guidance is a positive contract with required structural slots rather than a list of prohibitions — prohibition-shaped guidance measurably backfires on wrong-output-shape failures.

## What's inside

```
skills/functional-specification/
├── SKILL.md
├── references/
│   ├── requirement-anatomy.md
│   └── section-guide.md
├── templates/
│   ├── functional-spec.md
│   └── functional-spec-minimal.md
└── checklist.md
```

## Boundaries

This skill covers the functional-spec artifact only.

| Question | Skill |
|---|---|
| What must it observably do? | this skill |
| How will it be built? | [`software-design-docs`](https://github.com/mlwelles/software-design-docs) |
| Why build it, and for whom? | `prd-development` |
| What is the end-to-end experience? | `customer-journey-map` |
| In what order do we build it? | `superpowers:writing-plans` |

It uses `writing-copy` as a separately installed prose-quality dependency and defers diagrams to a dedicated diagram skill. This repository does not bundle `writing-copy`.

One rule deliberately contradicts `software-design-docs`: that skill says define terms inline and skip the glossary, while this one requires a Vocabulary section. A functional spec is a contract several parties read independently, and a term meaning one thing in clause 4 and another in clause 40 is the most common way a spec fails acceptance.

## Install

```bash
openskills install mlwelles/functional-specification/skills/functional-specification --global --universal
```

## License

MIT. See [LICENSE](LICENSE).
