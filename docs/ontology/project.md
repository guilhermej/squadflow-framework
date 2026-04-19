# Project

> A temporary initiative with a defined start, scope, and end — it delivers, is canceled, or is absorbed into a new Factory.

Projects are where the business changes: launch a product, migrate a system, open a market, rewrite a process. Each Project has a beginning (scope decided), a middle (Squad executes), and an end (outcome judged). When the outcome must then be operated continuously, the Project is **absorbed** into a new Factory — the most important transition in SquadFlow.

Distinct from a **Factory** (continuous, no end) and from a **Task** (atomic; a Project is many Tasks coordinated over weeks or months). SquadFlow does not tell you *how* to execute a Project — pick Scrum, Shape Up, Kanban — but insists Projects live in the same graph as Factories, Squads, and OKRs.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `name` | string | yes | Human-readable name. |
| `description` | string | no | Scope summary. |
| `company_id` | UUID | yes | Owning Company. |
| `brand_id` | UUID | no | Brand scope (optional). |
| `owner_id` | UUID (Player) | yes | Project Owner. |
| `squad_ids` | array of UUID | yes | Squads executing. |
| `okr_ids` | array of UUID | no | OKRs the Project contributes to. |
| `state` | enum | yes | `idea`, `scoping`, `backlog`, `active`, `delivery`, `closed`. |
| `close_reason` | enum | no | `delivered`, `canceled`, `absorbed` — set at close. |
| `absorbed_into_factory_id` | UUID | no | Set when `close_reason = absorbed`. |
| `start_date` / `end_date` | date | no | State dates. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/project.schema.json`](../data-model/schemas/).

## Relations

- Owned by a **Company**; optionally scoped to a **Brand**.
- Accountable to one **Player** (Project Owner).
- Executed by one or more **Squads**.
- Contributes to many **OKRs**.
- When absorbed, points to one **Factory** via `absorbed_into_factory_id`.
- Receives many **Tasks**; may have **Documents** attached.

## Lifecycle

`idea → scoping → backlog → active → delivery → closed`. At close, `close_reason` is one of:

- **`delivered`** — shipped; no ongoing operational load.
- **`canceled`** — abandoned before delivery.
- **`absorbed`** — shipped, and the outcome must be operated continuously; a new Factory is created and linked.

See [`../lifecycles/project.md`](../lifecycles/project.md).

## Example — a project absorbed into a factory

*Launch Partner Program* ships the legal, commercial, and operational machinery for a partner ecosystem: contract template, portal, onboarding flow, commission calculator. At close, none of those run themselves. Project closes with `close_reason = absorbed`, pointing to a new *Partner Operations* Factory (permanent kanban, Factory Manager named, Squad handed off). The Project is gone; the Factory runs forever.

## Antipatterns

- **Projects without an end date.** A Project that never closes is a Factory pretending to be a Project.
- **Skipping `scoping`.** The biggest source of failed Projects. Scoping is where the Owner negotiates timeline and deliverables.
- **Absorbing without creating the Factory.** If `close_reason = absorbed` and `absorbed_into_factory_id` is null, the absorption did not actually happen.
- **No OKR link.** If a Project cannot point to an OKR, ask whether it should exist.
