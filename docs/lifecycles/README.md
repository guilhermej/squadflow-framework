# Lifecycles

Every first-class entity in SquadFlow has a **state machine** — a finite list of states plus the named transitions between them. Lifecycle files in this folder document those machines.

Ambiguity about state is the leading cause of stalled work. Making state explicit, documented, and finite is one of the framework's five principles (see [MANIFESTO.md](../../MANIFESTO.md)).

## Reading a state diagram

Each lifecycle file opens with a Mermaid `stateDiagram-v2`. The conventions:

- **Rectangles** are states.
- **Arrows** are transitions, labeled with the triggering event (e.g., `scope → approve`).
- **`[*]`** is the implicit start/end — creation and deletion.
- **`⇄`** in prose indicates reversible transitions (e.g., `active ⇄ paused`).
- **Branches from a state** (e.g., `closed` → `delivered` / `canceled` / `absorbed`) are modeled as sub-states or captured in the `close_reason` attribute of the schema.

## File template

Every lifecycle file follows the same structure. If you edit or add one, match this template.

```markdown
# <Entity> Lifecycle

> One-sentence summary of the shape of the lifecycle.

## State diagram

<Mermaid stateDiagram-v2 here>

## States

| State | Description | Entry conditions | Exit conditions |

## Transitions

| From | To | Trigger | Actor | Validation | Side effects |

## State-dependent behavior

- When `<state>`: <what the system or framework does differently>
- ...

## Examples

Narrative walkthroughs (2–3) showing how a real entity moves through states.
```

## Index

| Entity | Lifecycle | Notes |
|---|---|---|
| [Company](company.md) | trivial | `active → archived`. |
| [Brand](brand.md) | trivial | `active → archived`. |
| [Player](player.md) | small | `candidate → active ⇄ on_leave → offboarded`. |
| [Document](document.md) | small | `draft → in_review → published ⇄ outdated → archived`. |
| [Task](task.md) | small | `todo → in_progress ⇄ blocked → done`. |
| [OKR](okr.md) | quarterly rhythm | `draft → active → in_review → closed` with scoring. |
| [Squad](squad.md) | team shape | `forming → active ⇄ on_hold → dissolving → dissolved`. |
| [Factory](factory.md) | operational | `proposed → active ⇄ paused → retired`. |
| [Project](project.md) | richest | `idea → scoping → backlog → active → delivery → closed` with `close_reason`. |

## Cross-references

- Every `state` enum value documented here must match exactly the corresponding JSON Schema at [`../data-model/schemas/<entity>.schema.json`](../data-model/schemas/). CI fails if they diverge.
- Transitions name **Roles** (Squad Lead, Factory Manager, Org Steward, …). Role definitions live in [`../processes/roles.md`](../processes/).
- Sensitive transitions (retiring a Factory, absorbing a Project, dissolving a Squad) create **decision-log entries** per [`../processes/governance.md`](../processes/).
