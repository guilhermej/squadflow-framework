# Squad

> A **Squad** is a cross-functional team of two or more Players responsible for one or more Factories or Projects.

## Purpose

Squads are the work-unit of SquadFlow. Where a Company is the legal frame, a Squad is the human frame — the team that actually runs a part of the business together. The term is borrowed from the Spotify model, but SquadFlow does not adopt Spotify's full structure (tribes, chapters, guilds). It keeps only the squad — a multi-skilled, durable team — because that is the abstraction that survived.

A Squad is durable but not permanent. It forms around a need, stays active for months or years, and dissolves when its mandate is no longer relevant. A Squad is distinct from a **Project**: a Project is a temporary initiative with a defined end; a Squad is a team that runs multiple projects and factories over time. One Squad typically runs one or two Factories plus any active Projects that fit its skill set.

A Squad is also distinct from a **department** or **function**. A department is hierarchical ("Engineering", "Marketing") and organized around craft. A Squad is organized around an outcome — shipping a product, closing deals for a brand, running customer success — and deliberately brings together the different crafts that outcome needs.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `e1f2a3b4-...` |
| `name` | string | yes | Human-readable name. | `Platform` |
| `description` | string | no | What the squad is responsible for. | `Runs core platform services...` |
| `company_id` | UUID | yes | Company that owns the Squad. | `<company-uuid>` |
| `brand_ids` | array of UUID | no | Brands the Squad serves (empty if cross-brand). | `["<brand-uuid>"]` |
| `lead_id` | UUID (Player) | yes | Squad Lead. | `<player-uuid>` |
| `member_ids` | array of UUID | yes | All Players on the Squad, including the Lead. | `[...]` |
| `state` | enum | yes | `forming`, `active`, `on_hold`, `dissolving`, `dissolved`. | `active` |
| `formed_on` | date | no | Date the Squad went active. | `2025-04-01` |
| `dissolved_on` | date | no | Set when dissolved. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/squad.schema.json`](../data-model/schemas/).

## Relations

- `Squad` ← owned_by ← `Company` (many to 1)
- `Squad` → serves → `Brand` (many to many, optional)
- `Squad` → led_by → `Player` (1 Squad Lead, many to 1)
- `Squad` → composed_of → `Player` (1 to many — members)
- `Squad` → responsible_for → `Factory` (1 to many — a Squad can run multiple Factories)
- `Squad` → responsible_for → `Project` (1 to many — a Squad can run multiple active Projects)
- `Squad` → contributes_to → `OKR` (many to many)

## Lifecycle

States: `forming → active ⇄ on_hold → dissolving → dissolved`. `forming` is the staffing phase. `active` is the default operating state. `on_hold` is reversible and usually temporary (a quarter without capacity). `dissolving → dissolved` captures the formal shutdown — members are reassigned, responsibilities transfer.

> See [`../lifecycles/squad.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — A product squad at a startup

At *Helios*, the *Platform* Squad has 6 members: 3 engineers, 1 designer, 1 PM, and the Squad Lead. It is responsible for the core platform Factory (*Platform Maintenance*, a permanent kanban of bugs/improvements) and the current *Billing Migration* Project. Members attend a 30-minute Squad Sync every Tuesday; the Squad Lead runs the weekly Factory Review and the Project Kickoff when a new project lands on the Squad's plate.

### Example 2 — A multi-brand content squad

At Grupo Solyd, the *Content* Squad works across three Brands (*Solyd*, *Caveiratech*, and *Mindz*), producing courses, articles, and videos. Its `brand_ids` lists all three. It runs one Factory per Brand (three distinct content pipelines) and picks up cross-Brand Projects (a new newsletter, a rebranding push). The Squad Lead coordinates with three different stewards — one per Brand — because the content cadence differs from brand to brand.

## Antipatterns

**Squads of one.** A Squad is at least two Players. A solo contributor running a Factory is not a Squad — they are a Player who has Factory Manager as a Role. Do not create Squads just to wrap a single person.

**Using Squads as reporting structure.** SquadFlow is orthogonal to HR reporting. A Player can be on a Squad whose Lead is not their HR manager. Do not flatten reporting lines into Squads — reporting lives outside the ontology.

**Permanent Squads.** Squads are durable but not permanent. If a Squad has been `active` for five years with no review, its mandate has probably drifted. Schedule a Squad-level retrospective annually and be willing to dissolve and re-form.

**Squad as a department.** A marketing Squad that only contains marketers is a department, not a Squad. A real Squad crosses crafts. If your Squad has one role per Player and one kind of work, rethink the composition.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Roles (Squad Lead): [`../processes/roles.md`](../processes/)
- Lifecycle: [`../lifecycles/squad.md`](../lifecycles/)
- Schema: [`../data-model/schemas/squad.schema.json`](../data-model/schemas/)
- Related entities: [Player](player.md), [Factory](factory.md), [Project](project.md)
