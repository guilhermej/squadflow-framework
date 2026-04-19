# Task

> A **Task** is an atomic unit of work assigned to a single Player, belonging to a Factory, Project, or Squad.

## Purpose

Tasks are the leaves of the work graph. A Factory's kanban is made of Task cards moving through stages. A Project's burndown is made of Tasks completing. A Squad's ad-hoc work — "review the draft", "prepare the quarterly report" — is also Tasks. SquadFlow keeps Tasks deliberately simple so that all the framework's complexity lives one level above them.

A Task is distinct from a **Project** — a Project is a coordinated body of many Tasks over weeks or months; a Task is one thing one person does. A Task is distinct from a **Document** — a Document is recorded knowledge; a Task is pending work. If you find yourself adding a "status" heading to a Document, you are reinventing Tasks.

A Task has exactly one parent. The parent type (`factory`, `project`, or `squad`) tells you why the Task exists. A Task on a Factory is a kanban card. A Task on a Project is part of the Project's execution. A Task on a Squad is a Squad-level chore that does not belong to any specific Factory or Project.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `c3d4e5f6-...` |
| `title` | string | yes | Short actionable title. | `Review the Stripe migration design doc` |
| `description` | string | no | Longer context, if needed. | `See design doc at...` |
| `parent_type` | enum | yes | `factory`, `project`, or `squad`. | `project` |
| `parent_id` | UUID | yes | ID of the parent Factory, Project, or Squad. | `<parent-uuid>` |
| `assignee_id` | UUID (Player) | yes | The Player responsible. | `<player-uuid>` |
| `state` | enum | yes | `todo`, `in_progress`, `blocked`, `done`. | `in_progress` |
| `done_reason` | enum | no | `completed` or `canceled` (set when `state = done`). | `null` |
| `due_date` | date | no | Target completion date. | `2026-05-10` |
| `estimate_hours` | number | no | Optional effort estimate. | `4` |
| `done_at` | datetime | no | Set when `state` becomes `done`. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/task.schema.json`](../data-model/schemas/).

## Relations

- `Task` ← belongs_to ← `Factory` / `Project` / `Squad` (many to 1, polymorphic via `parent_type` + `parent_id`)
- `Task` ← assigned_to ← `Player` (many to 1)

Tasks do not link directly to OKRs. The OKR contribution is inherited from the parent (Factory, Project, or Squad).

## Lifecycle

States: `todo → in_progress ⇄ blocked → done`. `blocked` is a first-class state — if work is waiting on someone or something external, it is `blocked`, not `in_progress`. When `done`, the `done_reason` is either `completed` (finished as intended) or `canceled` (abandoned without completing).

> See [`../lifecycles/task.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — A kanban card on a factory

*B2B Sales* Factory has a kanban with stages *Prospect → Qualified → Proposal Sent → In Negotiation → Won*. Each card is a Task whose `parent_type = factory` and `parent_id = <sales-factory-uuid>`. The Task's `assignee_id` is the Sales Development Rep or Account Executive in charge of that deal. Moving the card between stages maps to moving the Task through states — plus a change of assignee when handing off from SDR to AE.

### Example 2 — A task inside a project

The *Billing Migration* Project has dozens of Tasks: *"Write the Stripe connector"*, *"Migrate existing subscriptions"*, *"Write the rollback playbook"*, *"Set up monitoring"*. Each has `parent_type = project` and `parent_id = <billing-migration-uuid>`. Each is assigned to one Player. Some are `blocked` waiting on access to production data; others are `in_progress`. When the Project closes, remaining `todo` Tasks are either closed as `canceled` or moved to a successor Factory.

### Example 3 — A squad-level task

The *Platform* Squad has a Task: *"Prepare Q2 retrospective slides"*, `parent_type = squad`, `parent_id = <platform-squad-uuid>`, `assignee_id = <squad-lead>`. It does not belong to any specific Factory or Project — it is simply work the Squad needs done. Low ceremony, one assignee, due next Tuesday.

## Antipatterns

**Tasks with multiple assignees.** A Task has one `assignee_id`. If two people need to act, split into two Tasks. Shared responsibility is unowned responsibility.

**Tasks without a parent.** Every Task belongs to a Factory, a Project, or a Squad. An orphan Task is a Task that nobody is tracking. If a piece of work does not fit any of the three, ask whether it should exist at all — or create the parent before creating the Task.

**Over-decomposing Tasks.** A Task small enough to complete in 10 minutes is overhead, not work. Combine them into one Task of "review the three pull requests" rather than three Tasks of "review PR #1", "review PR #2", "review PR #3".

**Tasks stuck in `blocked` forever.** `blocked` is a temporary state. If a Task has been blocked for more than a week, escalate — either unblock it, cancel it, or convert it into a separate Project to address the underlying blocker.

**Using Task to track personal to-dos.** SquadFlow Tasks are organizational work, not personal reminders. Keep personal to-dos out of the work graph so that the graph remains a trustworthy map of what the organization is doing.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Lifecycle: [`../lifecycles/task.md`](../lifecycles/)
- Schema: [`../data-model/schemas/task.schema.json`](../data-model/schemas/)
- Related entities: [Factory](factory.md), [Project](project.md), [Squad](squad.md), [Player](player.md)
