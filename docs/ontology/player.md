# Player

> An individual who executes work in the organization — an employee, contractor, founder, or partner.

The human unit in SquadFlow. Every piece of work lands on a Player — through a Task, a role on a Squad, ownership of a Factory, accountability for a Project, or authorship of a Document. The word *Player* implies agency; SquadFlow encourages modeling freelancers, advisors, and core partners as Players too — anyone who executes.

A Player is distinct from a **Role**. A Role (Squad Lead, Factory Manager, Org Steward…) is a named responsibility; Players hold Roles. Roles live in [`../processes/roles.md`](../processes/roles.md), not as separate entities.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `full_name` | string | yes | Legal name (for contracts and payroll). |
| `display_name` | string | no | Day-to-day name. |
| `email` | string | yes | Primary work email. |
| `company_ids` | array of UUID | yes | Employing Companies. |
| `role_slugs` | array of enum | no | Roles held. |
| `state` | enum | yes | `candidate`, `active`, `on_leave`, `offboarded`. |
| `joined_on` / `offboarded_on` | date | no | Effective dates. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Sensitive HR data (compensation, performance reviews) is **not** in the ontology. Keep it in an HR system.

Authoritative list: [`../data-model/schemas/player.schema.json`](../data-model/schemas/).

## Relations

- Employed by one or more **Companies**.
- Member of zero or more **Squads**.
- Assignee of zero or many **Tasks**.
- Owner of zero or many **Documents**.
- Holds zero or more **Roles**.

## Lifecycle

`candidate → active ⇄ on_leave → offboarded`. Offboarded records are preserved for historical references; never deleted. See [`../lifecycles/player.md`](../lifecycles/player.md).

## Example

Ana signs her offer on 2026-01-20. Player record created with `state = candidate`. On her first day, state flips to `active`, she joins the *Platform* Squad. Six months later she becomes Squad Lead of a new *Onboarding* Squad; `role_slugs` grows to `["player", "squad_lead"]`.

## Antipatterns

- **Modeling job titles as Players.** "Senior Backend Engineer" is a job title, not a SquadFlow concept. SquadFlow cares what Squad someone is on and what Roles they hold.
- **Creating Players for teams.** A team is a Squad. A function is a Factory. If you cannot point at a human, do not model it as a Player.
- **Deleting offboarded Players.** Set `state = offboarded`. Tasks, Documents, and historical OKRs reference them.
