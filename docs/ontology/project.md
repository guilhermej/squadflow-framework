# Project

> A **Project** is a temporary initiative with a defined start, scope, and end — it either delivers an outcome, is canceled, or is absorbed into a new Factory.

## Purpose

Projects are where the business changes. Launch a new product. Migrate a billing system. Open a new market. Rewrite a sales process. Each Project has a beginning (the scope is decided), a middle (the Squad executes), and an end (the outcome is judged). When a Project's outcome needs to be run continuously after delivery, the Project is *absorbed* into a new Factory — the single most important transition in SquadFlow.

A Project is distinct from a **Factory** (see [Factory](factory.md)): a Factory produces the same output repeatedly with no end date; a Project produces one defined outcome and closes. A Project is distinct from a **Task** (see [Task](task.md)): a Task is an atomic unit of work; a Project is a coordinated body of many Tasks over weeks or months.

Projects are the workload that most frameworks handle well (Scrum, Shape Up, Kanban-for-projects). SquadFlow does not reinvent project execution inside a Project — pick the method you like — but it insists that Projects live in the same graph as Factories, Squads, and OKRs so the organization can reason about them as a whole.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `b2c3d4e5-...` |
| `name` | string | yes | Human-readable name. | `Billing Migration` |
| `description` | string | no | Scope summary. | `Migrate from custom billing to Stripe...` |
| `company_id` | UUID | yes | Owning Company. | `<company-uuid>` |
| `brand_id` | UUID | no | Brand-scoped Projects set this; cross-brand leave null. | `null` |
| `owner_id` | UUID (Player) | yes | Project Owner. | `<player-uuid>` |
| `squad_ids` | array of UUID | yes | Squads working on the Project. | `[...]` |
| `okr_ids` | array of UUID | no | OKRs the Project contributes to. | `[...]` |
| `state` | enum | yes | `idea`, `scoping`, `backlog`, `active`, `delivery`, `closed`. | `active` |
| `close_reason` | enum | no | `delivered`, `canceled`, `absorbed` (set at close). | `null` |
| `absorbed_into_factory_id` | UUID | no | Set when `close_reason = absorbed`. | `null` |
| `start_date` | date | no | Date the Project became `active`. | `2026-02-15` |
| `end_date` | date | no | Date the Project became `closed`. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/project.schema.json`](../data-model/schemas/).

## Relations

- `Project` ← owned_by ← `Company` (many to 1)
- `Project` ← scoped_to ← `Brand` (many to 1, optional)
- `Project` ← accountable_to ← `Player` (many to 1 — Project Owner)
- `Project` ← executed_by ← `Squad` (many to many)
- `Project` → contributes_to → `OKR` (many to many)
- `Project` → absorbed_into → `Factory` (0 or 1 — only when `close_reason = absorbed`)
- `Project` → receives → `Task` (1 to many)
- `Project` ← documented_by ← `Document` (many to many — decision logs, scope docs)

## Lifecycle

States: `idea → scoping → backlog → active → delivery → closed`. `idea` captures a raw proposal. `scoping` defines the shape (deliverables, timeline, required Squads). `backlog` means scoped and approved but not started. `active` is the execution phase. `delivery` is the short handover phase when the outcome is being reviewed, tested, and closed out. `closed` is terminal.

A closed Project carries a `close_reason`:

- `delivered` — shipped successfully; the outcome exists as designed.
- `canceled` — abandoned before delivery; no outcome, learnings may be recorded.
- `absorbed` — delivered, and the output must now be operated continuously. A new Factory is created; `absorbed_into_factory_id` points to it.

> See [`../lifecycles/project.md`](../lifecycles/) for the state diagram and full transition rules.

## Examples

### Example 1 — A project that delivers and closes

*Helios Corp.* runs a *Billing Migration* Project. Scope: move from a custom billing codebase to Stripe. The *Platform* Squad executes. The Project Owner is the VP of Engineering. Start: Feb 15. State progression: `idea` (CEO raises the concern in Jan) → `scoping` (Platform Squad sizes the work, three weeks) → `backlog` (approved; waits for Q2) → `active` (execution, three months) → `delivery` (two weeks of smoke testing in parallel with the old system) → `closed` with `close_reason = delivered`. The old billing code is removed; no Factory is created because Stripe handles operations.

### Example 2 — A project absorbed into a factory

The same company later runs *Launch Partner Program*. Scope: build the legal, operational, and commercial machinery for a partner ecosystem. The *Go-to-Market* Squad executes. At `delivery`, the Project has produced: a contract template, a partner portal, a partner onboarding process, a commission calculation routine. None of those run themselves. The Project closes with `close_reason = absorbed`, pointing to a brand-new Factory called *Partner Operations* — permanent kanban, Factory Manager named, Squad (or parts of the original Squad) handed off. The Project is gone; the Factory runs forever.

## Antipatterns

**Projects without an end date.** A Project with no end is a Factory pretending to be a Project. If it never closes, the work is continuous — model it as a Factory.

**Skipping `scoping`.** Jumping straight from `idea` to `active` is the biggest single source of failed Projects. The `scoping` phase is where the Project Owner negotiates timeline, deliverables, and Squad availability. Skipping it moves the uncertainty into the middle of execution.

**Projects with no OKR link.** If a Project cannot point to at least one OKR it contributes to, ask whether it should be happening at all. Some maintenance work legitimately has no OKR link; most "strategic initiatives" should.

**Absorbing a Project without creating the Factory.** If you say a Project was `absorbed` but `absorbed_into_factory_id` is null, the absorption did not happen — you just handed the work back to a Squad as a blob. Create the Factory, name the Manager, set the kanban stages, or mark the Project as `delivered` and accept that the ongoing work is unowned.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Roles (Project Owner): [`../processes/roles.md`](../processes/)
- Lifecycle: [`../lifecycles/project.md`](../lifecycles/)
- Schema: [`../data-model/schemas/project.schema.json`](../data-model/schemas/)
- Related entities: [Factory](factory.md), [Squad](squad.md), [OKR](okr.md), [Task](task.md)
