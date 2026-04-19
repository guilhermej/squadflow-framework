# Document

> A **Document** is recorded knowledge attached to one or more other entities — a manual, a policy, a decision log, an onboarding guide.

## Purpose

Documents exist so that the organization's knowledge does not live in a single head. A factory has a manual that teaches newcomers how to run it. A project has a decision log that records why certain trade-offs were made. A player has an onboarding doc. A company has a mission statement.

SquadFlow treats Documents as first-class so you can answer questions like *"what documents are attached to this Factory?"* or *"show me everything owned by Ana"* in one query. In a future proprietary system, Documents are rows in a table with a polymorphic `attached_to` relation; until then, they are pages in Notion, files in a repo, or links to external wikis.

A Document is distinct from a **Task**. A Task is work to be done. A Document is information that persists. If you find yourself updating a Document as a proxy for tracking work, split it: create Tasks for the work, keep the Document for the recorded outcome.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `d1e2f3a4-...` |
| `title` | string | yes | Descriptive title. | `Sales Factory Operating Manual` |
| `owner_id` | UUID (Player) | yes | Player accountable for keeping this Document correct. | `<player-uuid>` |
| `body_url` | string (URL) | no | Link to where the content lives (Notion page, repo path, external wiki). | `https://notion.so/...` |
| `body_markdown` | string | no | Inline Markdown body (alternative to `body_url`). | `# ...` |
| `attachments` | array of `{entity_type, entity_id}` | no | Polymorphic links to other entities. | See below |
| `state` | enum | yes | `draft`, `in_review`, `published`, `outdated`, `archived`. | `published` |
| `version` | string | no | Version or revision marker. | `v2.3` or `2026-03` |
| `published_at` | datetime | no | When the Document was first published. | ISO 8601 |
| `outdated_at` | datetime | no | Set when flagged `outdated`. | `null` |
| `archived_at` | datetime | no | Set when archived. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The `attachments` field is **polymorphic**: each entry has an `entity_type` (one of `company`, `brand`, `okr`, `factory`, `project`, `squad`, `task`, `player`) and an `entity_id`. A single Document can attach to many entities; a single entity can have many Documents.

Either `body_url` or `body_markdown` must be set. In v1.0, `body_url` is the common case — the actual content lives where it is authored (Notion, GitHub, an external wiki) and the Document record carries the metadata.

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/document.schema.json`](../data-model/schemas/).

## Relations

- `Document` ← owned_by ← `Player` (many to 1)
- `Document` → attached_to → `any entity` (many to many, polymorphic)

## Lifecycle

States: `draft → in_review → published ⇄ outdated → archived`. Two transitions matter most. Publishing marks the Document as canonical. Flagging `outdated` is an explicit signal to readers — "the content is stale, trust with care" — without deleting or hiding the record.

> See [`../lifecycles/document.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — Factory operating manual

The *Sales Factory* has a Document titled *Sales Factory Operating Manual*. It is attached to the Factory (`attachments = [{entity_type: "factory", entity_id: <sales-factory-uuid>}]`). The `owner_id` is the Factory Manager. When a new sales rep joins, onboarding points them here. When the sales process changes, the Factory Manager updates the Document and bumps `version`. If the Manager leaves and the Document has not been reviewed in six months, it is flagged `outdated` until the new Manager reviews and republishes.

### Example 2 — Project decision log

The *Billing Migration* Project records every major decision — *"why we chose Stripe over Adyen"*, *"why we delayed the EU launch"*, *"why we kept the old reports system"* — in a single Document attached to the Project (`attachments = [{entity_type: "project", entity_id: <project-uuid>}]`). The Project Owner owns the Document. When the Project closes (delivered, canceled, or absorbed), the Document stays linked for posterity and moves to `state = archived` only if the Project was canceled with no learnings worth preserving.

## Antipatterns

**Documents without an owner.** An unowned Document has nobody to keep it current. `owner_id` is required. If no single Player can own it, the scope is probably too broad — split the Document.

**Using Documents to track work.** If you catch yourself adding a "status" heading to a Document and updating it weekly, you are reinventing Tasks. Create Tasks on a Factory or Project; keep Documents for persistent, non-task content.

**Leaving stale content in `published`.** Publishing is a commitment to correctness. If you cannot confirm a Document is still accurate, flag it `outdated` explicitly — do not leave silent lies in `published`. The transition is one click; the lie is forever.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Lifecycle: [`../lifecycles/document.md`](../lifecycles/)
- Schema: [`../data-model/schemas/document.schema.json`](../data-model/schemas/)
- Related entities: [Player](player.md), [Factory](factory.md), [Project](project.md)
