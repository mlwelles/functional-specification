# Requirement Anatomy

## The block

```markdown
**FR-KEY-3** · `[assumed]`
A team administrator revokes a key. The key stops authenticating every
subsequent request, and requests already in flight complete.

- Revoked key authenticates no request issued after revocation.
- A request in flight at the moment of revocation completes normally.
- The revoking administrator and the revocation time appear in the audit record.
```

Four parts: ID, source marker, statement, criteria. The marker sits beside the ID so a reader meets the provenance and the requirement together.

## ID

`FR-<area>-<n>`. The area is a short word matching a Capabilities subsection: `FR-KEY-3`, `FR-BILLING-11`.

Assign once. Never renumber — IDs get quoted in tickets, test names, commit messages, and client email, and a renumbered spec silently invalidates all of them. Delete a requirement by marking it withdrawn and leaving the ID retired:

```markdown
**FR-KEY-7** · *withdrawn 2026-08-14, superseded by FR-KEY-12*
```

## Source marker

| Marker | Meaning | Obligation |
|---|---|---|
| `[brief]` | Stated in the brief or source material | none |
| `[decided: who, when]` | Someone with authority settled it | name them, so a reader can reopen it with the right person |
| `[assumed]` | The author invented it to make the spec coherent | list it in the Assumptions register |

Choose by asking where the requirement came from, not how confident you feel. A well-reasoned inference from the brief is still `[assumed]`.

`[decided]` needs a name. "Decided in the sync" tells a reader who disagrees nowhere to go.

## Statement

One observable behavior. Test it against three questions:

**Can someone verify this without reading the code?** If verifying requires inspecting internals, it is a design constraint, not a functional requirement.

**Does it name the actor?** "The key is revoked" hides who may revoke it — the exact question a reader has. "A team administrator revokes a key" answers it.

**Is it one behavior?** A statement joining two behaviors with "and" cannot fail cleanly; QA cannot report which half broke. Split it.

Avoid words with no test: fast, appropriate, reasonable, user-friendly, robust, as needed. Each is a measurement someone declined to make. Replace with the number, or mark the requirement `[assumed]` and put the number in the register where it will get settled.

## Criteria

Pass/fail conditions. Either inside the block (preferred — they stay adjacent to what they verify) or in a separate section where every criterion names its ID:

```markdown
- **FR-KEY-3** — a revoked key authenticates no request issued after revocation.
```

Cover three cases per requirement:

- the behavior succeeding
- the behavior refused, and how the refusal is observable
- the boundary — the empty set, the limit, the simultaneous actor

State outcomes, not mechanisms. "The refusal names the missing permission" is functional. "Returns `403` with an `insufficient_scope` body" is the design doc's to decide.

## Common defects

| Defect | Repair |
|---|---|
| Criteria listed as an independent section, citing no IDs | Move each criterion into its requirement, or prefix it with the ID |
| Invented value stated in the same voice as a sourced one | Mark `[assumed]`, register it |
| "The system shall support..." | Name the actor and the observable result |
| Two behaviors joined by "and" | Split into two IDs |
| Status codes, table names, endpoints in the statement | Restate as the observable outcome; the design doc owns the mechanism |
| A term used with two meanings across the document | Pin it once in Vocabulary, then use it identically |
