# Squad

> A cross-functional team of two or more Players responsible for one or more Factories or Projects.

Squads are the work-unit of SquadFlow. Where a Company is the legal frame, a Squad is the human frame — the team that actually runs a part of the business together. Term borrowed from the Spotify model, but SquadFlow only adopts the Squad — durable, multi-skilled, outcome-focused — not the rest (tribes, chapters, guilds).

A Squad is durable but not permanent. It forms around a need, runs for months or years, and dissolves when the mandate is no longer relevant. Distinct from a **Project** (which has a defined end) and from a **department** (which is organized around craft, not outcome).

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `name` | string | yes | Human-readable name. |
| `description` | string | no | Mandate. |
| `company_id` | UUID | yes | Owning Company. |
| `brand_ids` | array of UUID | no | Brands served (optional). |
| `lead_id` | UUID (Player) | yes | Squad Lead. |
| `member_ids` | array of UUID | yes | All members (including Lead). Minimum 2. |
| `state` | enum | yes | `forming`, `active`, `on_hold`, `dissolving`, `dissolved`. |
| `formed_on` / `dissolved_on` | date | no | State dates. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/squad.schema.json`](../data-model/schemas/).

## Relations

- Owned by one **Company**; optionally serves one or more **Brands**.
- Led by exactly one **Player** (Squad Lead).
- Composed of two or more **Players**.
- Responsible for one or more **Factories** and/or **Projects**.
- May scope **squad-level OKRs**; contributes to other OKRs.

## Lifecycle

`forming → active ⇄ on_hold → dissolving → dissolved`. See [`../lifecycles/squad.md`](../lifecycles/squad.md).

## Example

The *Platform* Squad at *Helios* has 6 members: 3 engineers, 1 designer, 1 PM, and the Squad Lead. It runs the *Platform Maintenance* Factory (bugs and small improvements, ongoing) and the current *Billing Migration* Project. Members attend a 30-minute Squad Sync every Tuesday; the Squad Lead runs the weekly Factory Review.

## Antipatterns

- **Squads of one.** Minimum two. A solo contributor running a Factory is a Player with the `factory_manager` role, not a Squad.
- **Squads as reporting structure.** HR reporting is orthogonal to Squads. A Player can be on a Squad whose Lead is not their HR manager.
- **Permanent Squads without review.** Squads are durable, not permanent. Annual retrospective; dissolve when mandate drifts.
- **Squads as departments.** A Squad crosses crafts. One role per member = a department, not a Squad.
