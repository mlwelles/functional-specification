# Pre-Share Checklist

Run before sending a functional specification to anyone. Each item names the failure it catches.

## Requirements

- [ ] Every requirement has an ID, a source marker, a statement, and criteria.
- [ ] No ID has been renumbered since the last version; withdrawn requirements keep their retired IDs.
- [ ] Every statement names its actor.
- [ ] No statement joins two behaviors with "and."
- [ ] No statement contains fast, appropriate, reasonable, user-friendly, robust, or as needed.
- [ ] Every requirement is verifiable by someone with no access to the code.

## Traceability

- [ ] Every criterion sits inside a requirement block or names the ID it verifies.
- [ ] No criterion floats in an independent list citing nothing.
- [ ] Every requirement has at least one criterion covering refusal, not only success.

## Provenance

- [ ] Every `[assumed]` requirement appears in the Assumptions register.
- [ ] Every register entry states what changes if the question is settled differently.
- [ ] Every `[decided]` marker names a person, not a meeting.
- [ ] No invented value is stated in the same unmarked voice as a brief-sourced one.
- [ ] `[assumed]` requirements do not outnumber `[brief]` and `[decided]` combined — if they do, the register goes out as a question list before this document does.

## Scope

- [ ] Every sentence passes the scope test: two different implementations could satisfy it.
- [ ] No schema, endpoint, status code, storage choice, or algorithm appears outside an externally-fixed interface, and each of those names the external source.

## Vocabulary

- [ ] Every contested term is defined once and used identically throughout.
- [ ] No term carries two meanings across sections.

## Completeness

- [ ] Error and edge behavior covers the empty set, the limit exactly reached, and two actors acting at once.
- [ ] Every entity with a lifecycle lists its illegal transitions, not only its legal ones.
- [ ] Out of scope distinguishes deferred from permanent.
- [ ] Any omitted section is marked omitted, with a reason.

## Prose

- [ ] Passed `writing-clearly-and-concisely` and `technical-writing-density`.
- [ ] The opening explains the problem before the first requirement.
