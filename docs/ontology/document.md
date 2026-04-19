# Document

> Recorded knowledge attached to one or more other entities — manuals, policies, decision logs, onboarding guides.

Documents exist so the organization's knowledge does not live in a single head. A Factory has a manual; a Project has a decision log; a Player has onboarding; a Company has a mission statement. SquadFlow makes Documents first-class so you can ask *"what documents are attached to this Factory?"* or *"show me everything owned by Ana"* in one query.

A Document is distinct from a **Task**. A Task is pending work; a Document is recorded outcome. If you find yourself updating a Document as a status tracker, split it: create Tasks for the work, keep the Document for the record.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `title` | string | yes | Descriptive title. |
| `owner_id` | UUID (Player) | yes | Player accountable for correctness. |
| `body_url` *or* `body_markdown` | string | yes (one of) | Content location or inline. |
| `attachments` | array of `{entity_type, entity_id}` | no | Polymorphic links. |
| `state` | enum | yes | `draft`, `in_review`, `published`, `outdated`, `archived`. |
| `version` | string | no | Revision marker (semver or date). |
| `published_at` / `outdated_at` / `archived_at` | datetime | no | State timestamps. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

The `attachments` field is polymorphic: each entry has `entity_type` (one of the nine entities) and `entity_id`.

Authoritative list: [`../data-model/schemas/document.schema.json`](../data-model/schemas/).

## Relations

- Owned by exactly one **Player**.
- Attached to any number of other entities (polymorphic).

## Lifecycle

`draft → in_review → published ⇄ outdated → archived`. The `outdated` state is a first-class flag — stale content is marked explicitly, not hidden. See [`../lifecycles/document.md`](../lifecycles/document.md).

## Example

The *Sales Factory* has a Document titled *Sales Factory Operating Manual*, attached to the Factory, owned by the Factory Manager. When the sales process changes, the Manager revises, bumps `version`, and republishes. If the Manager leaves and the doc goes unreviewed for six months, it is flagged `outdated` until the new Manager reviews and republishes.

## Antipatterns

- **Unowned Documents.** `owner_id` is required — without one, the doc goes stale.
- **Documents as status trackers.** Use Tasks. Documents are for persistent content, not evolving status.
- **Leaving stale content in `published`.** If you cannot confirm accuracy, flag `outdated`. The transition is one click; the lie is forever.
