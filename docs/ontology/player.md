# Player

> A **Player** is an individual who executes work in the organization — an employee, contractor, founder, or partner.

## Purpose

A Player is the human unit in SquadFlow. Every piece of work that matters lands on a Player at some point — through a Task, a role on a Squad, ownership of a Factory, accountability for a Project, or authorship of a Document.

Calling people *Players* (rather than *employees*, *users*, or *resources*) is deliberate. It implies agency and autonomy: a Player is on the field making decisions, not a spreadsheet row being assigned to. The framework encourages you to model freelancers, advisors, and core partners as Players too — anyone who executes, not just W-2 staff.

A Player is distinct from a **Role**. A Role (Squad Lead, Factory Manager, OKR Sponsor, Org Steward…) is a *responsibility*, not a person. One Player can hold several Roles at once. Roles are documented in [`../processes/roles.md`](../processes/roles.md), not as separate entities in the ontology.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `c1d2e3f4-...` |
| `full_name` | string | yes | Legal name, for contracts and payroll. | `Ana Beatriz Silva` |
| `display_name` | string | no | Name used in day-to-day (falls back to `full_name`). | `Ana Silva` |
| `email` | string | yes | Primary work email. | `ana@helios.co` |
| `company_ids` | array of UUID | yes | Companies that employ or engage this Player. | `["a1b2c3..."]` |
| `role_slugs` | array of string | no | Roles held (e.g. `["squad_lead", "okr_sponsor"]`). | `[]` |
| `state` | enum | yes | `candidate`, `active`, `on_leave`, `offboarded`. | `active` |
| `joined_on` | date | no | Effective start date. | `2025-09-01` |
| `offboarded_on` | date | no | Set when `state` becomes `offboarded`. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/player.schema.json`](../data-model/schemas/).

Note: sensitive HR attributes (compensation, personal documents, performance reviews) are **not** in the ontology. Keep them in a dedicated HR system. The Player record is about *where this person fits in the work graph*, not about the employment relationship itself.

## Relations

- `Player` ← employed_by ← `Company` (many to many — most Players belong to exactly one Company, but contractors and shared founders can span multiple)
- `Player` ∈ `Squad` (many to many — a Player can belong to multiple Squads)
- `Player` ← assigned_to ← `Task` (many to many from Task's side)
- `Player` → owns → `Document` (1 to many — a Player can own many Documents)
- `Player` → holds → Role (many to many, via `role_slugs`)

## Lifecycle

States: `candidate → active ⇄ on_leave → offboarded`. Candidates appear before contract signing; active is the default; on_leave is reversible (parental leave, sabbatical); offboarded is terminal but the record stays as historical reference.

> See [`../lifecycles/player.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — A new engineer joining a squad

Ana accepts an offer at *Helios*. The operations team creates a Player record with `state = candidate`, `joined_on = 2026-05-01`. On her first day, the state flips to `active`, she is added to the *Platform* Squad as a member, and her `role_slugs = ["player"]`. Six months later, she is promoted to Squad Lead of a new *Onboarding* Squad. Her Player record now has `role_slugs = ["player", "squad_lead"]` — she keeps her membership in *Platform* and adds leadership of *Onboarding*.

### Example 2 — A founder wearing many hats

The founder of a small multi-brand group is a Player with `role_slugs = ["org_steward", "okr_sponsor", "factory_manager"]`. They are the steward of one Company, sponsor of three OKRs, and manager of one Factory. As the group grows, they shed roles — first the factory management, then the OKR sponsorship — keeping only `org_steward`. Their Player record stays the same; only the roles change.

## Antipatterns

**Using Player to model org chart or job titles.** Players are individuals, not roles or job titles. "Senior Backend Engineer" is a compensation/HR concept, not a SquadFlow concept. SquadFlow cares what Squad they're in and what Roles they hold.

**Creating Players for abstract functions.** "The marketing team" is not a Player — it is a Squad. "Customer support" is not a Player — it is a Factory. If you cannot point at one human being, do not model it as a Player.

**Deleting offboarded Players.** Historical tasks, OKRs, and documents reference the Player. Set `state = offboarded` instead of deleting. The record stays; active membership does not.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Roles: [`../processes/roles.md`](../processes/)
- Lifecycle: [`../lifecycles/player.md`](../lifecycles/)
- Schema: [`../data-model/schemas/player.schema.json`](../data-model/schemas/)
- Related entities: [Squad](squad.md), [Task](task.md), [Company](company.md)
