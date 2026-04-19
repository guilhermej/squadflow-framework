# Task

> An atomic unit of work assigned to a single Player, belonging to a Factory, Project, or Squad.

Tasks are the leaves of the work graph. A Factory's kanban is made of Task cards; a Project's execution is a set of Tasks; a Squad's ad-hoc work is Tasks. SquadFlow keeps Tasks deliberately simple — complexity lives one layer up, in Factories and Projects.

A Task has exactly one parent (via `parent_type` + `parent_id`) and exactly one assignee. Distinct from a **Project** (a coordinated body of Tasks) and from a **Document** (recorded outcome, not pending work).

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `title` | string | yes | Short actionable title. |
| `description` | string | no | Longer context. |
| `parent_type` | enum | yes | `factory`, `project`, or `squad`. |
| `parent_id` | UUID | yes | ID of the parent. |
| `assignee_id` | UUID (Player) | yes | The Player responsible. |
| `state` | enum | yes | `todo`, `in_progress`, `blocked`, `done`. |
| `done_reason` | enum | no | `completed` or `canceled` (when `done`). |
| `due_date` | date | no | Target completion. |
| `estimate_hours` | number | no | Optional effort estimate. |
| `done_at` / `created_at` / `updated_at` | datetime | yes/no | Record timestamps. |

Authoritative list: [`../data-model/schemas/task.schema.json`](../data-model/schemas/).

## Relations

- Belongs to exactly one **Factory**, **Project**, or **Squad** (polymorphic).
- Assigned to exactly one **Player**.

OKR contribution is inherited from the parent — Tasks do not link directly.

## Lifecycle

`todo → in_progress ⇄ blocked → done`. `blocked` is a first-class state — if work is waiting on external input, it is `blocked`, not `in_progress`. See [`../lifecycles/task.md`](../lifecycles/task.md).

## Example

The *Billing Migration* Project has dozens of Tasks: *"Write the Stripe connector"*, *"Migrate existing subscriptions"*, *"Set up monitoring"*. Each has `parent_type = project` and `parent_id = <billing-migration-uuid>`. Each is assigned to one Player. Some sit in `blocked` waiting on production access; others are `in_progress`.

## Antipatterns

- **Multiple assignees.** Split into separate Tasks. Shared ownership is unowned.
- **Tasks without a parent.** Every Task belongs to a Factory, Project, or Squad. Orphans are untracked.
- **Over-decomposing.** A 10-minute Task is overhead, not work. Combine.
- **Tasks stuck in `blocked` for weeks.** Escalate — unblock, cancel, or spawn a Project to fix the blocker.
- **Personal to-dos as Tasks.** Keep the work graph trustworthy; personal reminders live elsewhere.
