# Functional Specification: <feature>

**Status:** draft · **Author:** <name> · **Last updated:** <date>

## 1. Purpose and scope

<The problem, in ordinary language. What breaks today, for whom, and what it costs
them. Two or three paragraphs, no requirements yet.>

**In scope:** <the boundary of this release>

## 2. Actors

| Actor | Goal | Authority |
|---|---|---|
| <role> | <what they are trying to accomplish> | <what they may and may not do> |

## 3. Vocabulary

**<Term>** — <definition>. <Rejected synonym, if one competes.>

## 4. Capabilities

### 4.1 <Area>

**FR-<AREA>-1** · `[brief]`
<One observable behavior, active voice, naming the actor.>

- <criterion: the behavior succeeding>
- <criterion: the behavior refused, and how the refusal is observable>
- <criterion: the boundary — empty set, limit, simultaneous actors>

**FR-<AREA>-2** · `[assumed]`
<Statement.>

- <criterion>

## 5. Business rules

**BR-1** — <constraint holding across capabilities>. Governs FR-<AREA>-1, FR-<AREA>-4.

## 6. States and transitions

**<Entity>**

| From | To | Trigger | Actor |
|---|---|---|---|
| <state> | <state> | <event> | <actor> |

Illegal: <transition that must never occur>.

## 7. Error and edge behavior

| Condition | Observable outcome |
|---|---|
| <what goes wrong> | <what the actor sees; what persists; what does not> |

## 8. Assumptions register

- **FR-<AREA>-2** — <the question to settle>. <Why this answer was chosen.>
  <What changes if it is settled differently.>

## 9. Out of scope

- <exclusion> — <why, and whether it is deferred or permanent>
