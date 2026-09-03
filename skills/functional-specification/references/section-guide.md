# Section Guide

Nine sections, in the order the SKILL states. Each entry gives what the section is for, what makes it fail, and when it may be dropped.

## 1. Purpose and scope

The problem, the users, the boundary of this release — a few paragraphs of ordinary language before any requirement.

A reader opening the spec cold cannot evaluate requirements before understanding the problem. Name the concrete consequence, not the abstraction: "access dies with the employee who created it" beats "key ownership model is insufficient."

Never drop. A spec that opens on requirements forces every reader to reverse-engineer the problem from its tests.

## 2. Actors

Every party the system distinguishes: human roles, other systems, scheduled processes. For each, one line on their goal and one on their authority.

Fails when it lists roles without authority. "Administrator" tells a reader nothing; "administrator — may issue and revoke keys for their own team, not other teams" is the fact the requirements depend on.

Include non-human actors. A nightly job that expires records is an actor, and its behavior needs requirements like any other.

## 3. Vocabulary

Every domain term the requirements depend on, defined once.

Include a term when readers could reasonably differ on it, when it has a narrower meaning here than in ordinary use, or when two candidate words compete (key/token/credential — pick one, note the rejected synonyms).

Fails when it defines dictionary words and skips the contested ones. The test is not "is this word technical" but "could two readers apply this differently."

May shrink to a handful of entries. Never drop: this section is why `software-design-docs` waives the glossary and this skill requires it.

## 4. Capabilities

The requirement blocks, grouped into areas that match the ID prefixes. This is the bulk of the document.

Order areas by the sequence a user meets them, not by implementation convenience.

Fails when grouped by system component rather than by capability. A reader looking for "what can an administrator do with a key" should find it in one place, not split across three subsystems.

Anatomy of a block → `requirement-anatomy.md`.

## 5. Business rules

Constraints that hold across capabilities rather than inside one: limits, precedence between conflicting permissions, retention periods, exclusivity.

A rule belongs here when repeating it in every affected requirement would be noise. Give it an ID (`BR-<n>`) and cite it from the requirements it governs.

Fails when it restates a requirement. If exactly one capability is affected, it is a requirement, not a rule.

Drop when genuinely empty, and say so.

## 6. States and transitions

For each entity with a lifecycle: the states, the legal transitions with their trigger and actor, and the illegal ones.

Name the illegal transitions explicitly. "A revoked key cannot return to active" is the requirement a reader most needs and the one most often left implicit.

A table of from/to/trigger/actor beats prose. A diagram may accompany it; defer the drawing to `mermaid-diagrams` and keep the table authoritative, since the table is what QA reads.

Drop when no entity has more than one state.

## 7. Error and edge behavior

What the system does when things go wrong or arrive at a boundary: refused actions, absent data, exhausted limits, contending actors, unavailable dependencies.

State observable outcomes — what the actor sees, what persists, what does not. Mechanism belongs to the design doc.

Fails by covering only refusals. The neglected cases are the empty set, the single element, the limit exactly reached, and two actors acting at once.

Never drop. A spec silent on failure gets its failure behavior invented during implementation, where nobody reviews it.

## 8. Assumptions register

Every `[assumed]` requirement, collected by ID, each with the question a reader must settle and the consequence of settling it differently.

```markdown
- **FR-KEY-5** — is 50 keys the right cap? Chosen to keep the revocation list
  reviewable. A materially higher cap changes nothing else; removing the cap
  withdraws FR-KEY-5 and its criteria.
```

Fails as a bare list of assumptions with no IDs and no consequence. The register exists so a reviewer can settle every open question in one pass and know what each answer costs.

Empty register on a spec written from a thin brief means the assumptions were made silently, not that none were made.

## 9. Out of scope

What this release deliberately excludes, and one clause on why.

Bounds what a reader assumes is coming. Distinguish "not in this release" from "not ever" — they set different expectations.

Fails when it lists things nobody expected. Name only the exclusions a reasonable reader would otherwise assume are included.
