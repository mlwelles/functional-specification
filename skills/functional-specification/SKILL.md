---
name: functional-specification
description: Use when writing, structuring, or reviewing a functional specification — a document stating what a system must observably do, for engineers, QA, and stakeholders who will accept the work. Applies when a brief, feature request, or set of decisions must become testable requirements with acceptance criteria. This skill is for the functional-spec artifact — not the technical design (see software-design-docs), not the product case for building it (see prd-development), not the end-to-end experience (see customer-journey-map), not the build sequence (see superpowers:writing-plans).
---

# Functional Specification

## Purpose

A functional specification states what a system must observably do, precisely enough that an engineer can build it, QA can test it, and a stakeholder can accept or reject the result. It answers *what, exactly, and how do we know it is right* — never *how it is built*.

Its readers disagree about the system. The spec's job is to make that disagreement visible before implementation, not to paper over it with confident prose.

## The requirement contract

Every requirement carries four parts. A requirement missing any one of them is not finished.

| Part | Rule |
|---|---|
| **ID** | `FR-<area>-<n>`, assigned once and never renumbered. Deleted requirements leave their ID retired, not reused. |
| **Statement** | One observable behavior. Active voice, naming the actor. Testable by someone with no access to the code. |
| **Source** | `[brief]`, `[decided: who, when]`, or `[assumed]`. Required on every requirement. |
| **Criteria** | Pass/fail conditions, stated with the requirement or citing its ID. |

Full anatomy with worked examples → `references/requirement-anatomy.md`.

### Why `Source` is mandatory

Writing a spec from an incomplete brief forces invention. Invention is fine; disguising it is not. The `Source` marker records, at the point of use, whether a requirement came from the brief, from a decision someone made, or from the author's own guess.

An `[assumed]` requirement is an open question wearing the costume of a decision. Mark it, then list every one in the Assumptions register so a reviewer can settle them in a single pass. Never carry an assumption only in a prefatory section — a reader meeting the requirement will not go looking.

### When assumptions outnumber sourced requirements

Draft the spec. Then count. If `[assumed]` requirements outnumber `[brief]` and `[decided]` combined, the brief cannot support a specification yet — stop and send the Assumptions register on its own, as a numbered question list, before circulating the document.

A register longer than roughly a dozen entries is not reviewable in one pass, and a spec resting on it invites line-by-line argument over invented details rather than a decision on the few questions that matter. Sending the questions first costs one round trip. Sending the full spec first costs a rewrite.

### Why criteria cite IDs

Criteria that float free of requirements cannot be traced. QA cannot map coverage, a changed requirement never flags its stale criterion, and a reviewer cannot cite one line. Either write criteria inside the requirement block, or make every criterion name the ID it verifies.

## The scope test

Apply to every sentence: **could two different implementations both satisfy this?**

- *Yes* → functional. Keep it. "The request is refused, and the refusal names the missing permission."
- *No* → design. Move it to the design doc. "The request returns `403 insufficient_scope`."

Schemas, endpoints, status codes, storage, and algorithms are design decisions. Naming them in a functional spec over-constrains the builder and duplicates a document that owns them properly.

Exception: when an interface is *externally fixed* — a published API contract, a regulatory format, a third-party integration — the exact shape is a functional requirement, because no other implementation satisfies the obligation. State the constraint and its source.

## Document shape

Sections in this order. Omit a section only when it is genuinely empty, and say so.

1. **Purpose and scope** — the problem, the users, the boundary
2. **Actors** — each actor, their goal, their authority
3. **Vocabulary** — every domain term the requirements depend on
4. **Capabilities** — the requirement blocks, grouped by area
5. **Business rules** — constraints cutting across capabilities
6. **States and transitions** — lifecycles, with legal and illegal moves
7. **Error and edge behavior** — what happens when things go wrong
8. **Assumptions register** — every `[assumed]` requirement, by ID
9. **Out of scope** — what this release does not do

Per-section guidance → `references/section-guide.md`. Templates → `templates/functional-spec.md`, `templates/functional-spec-minimal.md`. Before sharing → `checklist.md`.

## Vocabulary is a required section here

`software-design-docs` says define terms inline and skip the glossary. A functional spec inverts that rule deliberately. Its requirements are a contract several parties read independently, and a term meaning one thing in clause 4 and another in clause 40 is the most common way a spec fails acceptance. Pin each term once, then use it identically everywhere.

## Boundaries with adjacent skills

| Question | Skill |
|---|---|
| What must it observably do? | this skill |
| How will it be built? | `software-design-docs` |
| Why build it, and for whom? | `prd-development` |
| What is the end-to-end experience? | `customer-journey-map` |
| In what order do we build it? | `superpowers:writing-plans` |

Read and apply `writing-copy` before drafting the specification. This skill owns content and format; prose edits must preserve requirements, scope, constraints, and uncertainty.
