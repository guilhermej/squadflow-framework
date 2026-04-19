# Factory

> A **Factory** is a unit of continuous production — a permanent kanban that produces the same kind of outcome, over and over, as long as the business needs it.

## Purpose

Most companies get Factories wrong. They either treat continuous work as a backlog of tasks (no cadence, no ownership) or force it into sprint-based frameworks built for change work (artificial deadlines for work that never ends). SquadFlow makes Factories a first-class entity so that continuous operations have their own shape: a permanent kanban, a named Manager, a weekly review cadence, and explicit governance around starting, pausing, and retiring.

A Factory is distinct from a **Project**. A Factory produces the *same* output repeatedly — sales calls closed, articles published, support tickets resolved, candidates hired, invoices generated. It has no end. A Project produces *one* output and then closes. When a Project succeeds and its output needs to be operated forever, the Project is *absorbed* into a new Factory (see [Project](project.md)).

A Factory is distinct from a **Squad**. A Squad is a team; a Factory is a production system. One Squad typically runs one or two Factories. One Factory is run by exactly one Squad.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `a2b3c4d5-...` |
| `name` | string | yes | Human-readable name. | `B2B Sales` |
| `description` | string | no | What the Factory produces and how. | `Outbound pipeline for enterprise cybersecurity contracts` |
| `company_id` | UUID | yes | Owning Company. | `<company-uuid>` |
| `brand_id` | UUID | no | Owning Brand (if brand-scoped). | `null` or `<brand-uuid>` |
| `squad_id` | UUID | yes | Squad responsible for running this Factory. | `<squad-uuid>` |
| `manager_id` | UUID (Player) | yes | Factory Manager. | `<player-uuid>` |
| `kanban_stages` | array of string | yes | Ordered stage names of the kanban. | `["Prospect", "Qualified", "Proposal", "Won"]` |
| `state` | enum | yes | `proposed`, `active`, `paused`, `retired`. | `active` |
| `proposed_on` | date | no | Date the Factory was proposed. | `2025-02-10` |
| `activated_on` | date | no | Date it began producing. | `2025-03-01` |
| `paused_on` | date | no | Current pause start date (nullable). | `null` |
| `retired_on` | date | no | Set when retired. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/factory.schema.json`](../data-model/schemas/).

## Relations

- `Factory` ← owned_by ← `Company` (many to 1)
- `Factory` ← scoped_to ← `Brand` (many to 1, optional)
- `Factory` ← run_by ← `Squad` (many to 1)
- `Factory` ← managed_by ← `Player` (many to 1 — Factory Manager)
- `Factory` → contributes_to → `OKR` (many to many)
- `Factory` → receives → `Task` (1 to many — kanban cards are Tasks)
- `Factory` ← documented_by ← `Document` (many to many — manuals, SOPs)

## Lifecycle

States: `proposed → active ⇄ paused → retired`. A Factory is proposed, activated when it starts producing, paused if temporarily inactive (a quarter without demand, a key Player on leave), and retired when the business no longer needs the output. `retired` is terminal; historical records stay. Retiring a Factory requires approval from the Org Steward and the Factory Manager.

> See [`../lifecycles/factory.md`](../lifecycles/) for the state diagram and transition rules.

## Examples

### Example 1 — The sales factory

*Helios Corp.* runs a *B2B Sales* Factory with five kanban stages: `Prospect`, `Qualified`, `Proposal Sent`, `In Negotiation`, `Won` (plus a terminal `Lost` that is not a forward stage but a closure). The Factory Manager is the Head of Sales. The Squad running the Factory is the *Sales* Squad (3 SDRs, 2 account executives, 1 marketer embedded). Cards flow from left to right; a single "Won" card lives about 40 days on average. The Factory's weekly Factory Review walks the board left to right, identifies stuck cards, and reassigns owners if needed.

### Example 2 — The certified-students factory

At Grupo Solyd, the *Certified Students* Factory (Solyd brand) takes enrollees and produces certified graduates. Its kanban stages are the course phases: `Enrolled`, `Module 1 complete`, `Module 2 complete`, `Project submitted`, `Certified`. Each card is a student cohort. The Factory Manager runs a bi-weekly review. When engagement drops in one stage, the Factory proposes a Project — *"Improve Module 2 retention"* — that, when delivered, updates the Factory's materials and process. The Project closes; the Factory continues.

## Antipatterns

**Confusing a Factory with a backlog.** A backlog is an unordered pile of tasks. A Factory is a structured pipeline with named stages and a Manager. If you open the kanban and cannot explain what the stages mean, you have a backlog, not a Factory.

**Factories with no cadence.** A Factory without a weekly review becomes invisible. Stuck cards pile up; stages blur; nobody notices. Every active Factory has a weekly Factory Review on the calendar, owned by the Factory Manager.

**Short-lived Factories.** A Factory is permanent by design. If you find yourself creating a Factory that you expect to retire in three months, you are probably modeling a Project — use Project instead.

**Factories with ambiguous ownership.** A Factory has exactly one Manager. "The team owns it" is not ownership. Pick a person.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Roles (Factory Manager): [`../processes/roles.md`](../processes/)
- Lifecycle: [`../lifecycles/factory.md`](../lifecycles/)
- Schema: [`../data-model/schemas/factory.schema.json`](../data-model/schemas/)
- Related entities: [Project](project.md), [Squad](squad.md), [Task](task.md)
