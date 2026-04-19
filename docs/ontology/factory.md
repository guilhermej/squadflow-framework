# Factory

> A unit of continuous production — a permanent kanban that produces the same kind of outcome, repeatedly, as long as the business needs it.

Most companies get Factories wrong: they treat continuous work as an unstructured backlog, or force it into sprint-based frameworks built for change. SquadFlow makes Factories first-class so continuous operations have their own shape — a permanent kanban, a named Manager, a weekly Review, explicit governance around starting, pausing, and retiring.

Distinct from a **Project** (which has a defined end) and from a **Squad** (a team that *runs* Factories). One Squad typically runs one or two Factories; a Factory is run by exactly one Squad.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `name` | string | yes | Human-readable name. |
| `description` | string | no | What it produces. |
| `company_id` | UUID | yes | Owning Company. |
| `brand_id` | UUID | no | Owning Brand (optional). |
| `squad_id` | UUID | yes | Squad responsible. |
| `manager_id` | UUID (Player) | yes | Factory Manager. |
| `kanban_stages` | array of string | yes | Stages in order (minimum 2). |
| `state` | enum | yes | `proposed`, `active`, `paused`, `retired`. |
| `proposed_on` / `activated_on` / `paused_on` / `retired_on` | date | no | State dates. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/factory.schema.json`](../data-model/schemas/).

## Relations

- Owned by a **Company**; optionally scoped to a **Brand**.
- Run by exactly one **Squad**; managed by exactly one **Player** (Factory Manager).
- Contributes to many **OKRs**.
- Receives many **Tasks** (kanban cards).
- May have **Documents** attached (operating manuals, SOPs).

## Lifecycle

`proposed → active ⇄ paused → retired`. Retirement requires Steward + Manager approval and creates a decision-log entry. See [`../lifecycles/factory.md`](../lifecycles/factory.md).

## Example

*Helios Corp.* runs a *B2B Sales* Factory with stages `Prospect → Qualified → Proposal Sent → In Negotiation → Won`. The Factory Manager is the Head of Sales. The *Sales* Squad (3 SDRs, 2 AEs, 1 embedded marketer) runs the kanban. A weekly Factory Review walks the board left to right and reassigns stuck cards.

## Antipatterns

- **Confusing a Factory with a backlog.** A backlog is an unordered pile. A Factory has named stages and a Manager.
- **Factories with no cadence.** Weekly Factory Review is mandatory while active — otherwise the Factory becomes invisible.
- **Short-lived Factories.** If you expect to retire in three months, it is a Project.
- **Ambiguous ownership.** One Manager. "The team owns it" is not ownership.
