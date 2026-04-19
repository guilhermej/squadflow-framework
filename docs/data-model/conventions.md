# Data Model Conventions

Rules that every entity schema and every implementation of SquadFlow must follow. They exist to keep the model consistent across files, across languages (EN/PT), and across future client implementations (Python, TypeScript, Go, etc.).

## 1. Casing

- Field names: `snake_case` (e.g., `owner_id`, `kanban_stages`, `launched_on`).
- Enum values: `lowercase_snake_case` (e.g., `in_progress`, `on_hold`, `partially_met`).
- Entity names (in prose, titles, filenames): `PascalCase` for the entity itself (*Project*), `lowercase` for the file (`project.md`, `project.schema.json`).
- URLs and slugs in documentation: `kebab-case` (e.g., `vs-scrum.md`, `getting-started.md`).

## 2. Identifiers

- Every entity has an `id` field of type `string` with `format: "uuid"` (UUID v4).
- Foreign keys follow the pattern `<entity>_id` (`company_id`, `owner_id`, `parent_id`).
- Many-to-many relations use arrays with the plural: `<entity>_ids` (`squad_ids`, `okr_ids`).
- **Never** reuse UUIDs across entities — a Company, a Brand, and a Project with the same UUID would be a modeling bug.

## 3. Timestamps

- `created_at` and `updated_at` are **required** on every entity. Type: `string`, `format: "date-time"` (ISO 8601 UTC).
- State-transition timestamps are lowercase_snake_case with an `_at` suffix when they represent the exact moment, or `_on` when they represent the calendar date only (`archived_at`, `launched_on`, `paused_on`, `done_at`).
- All datetimes are stored in UTC. Clients render in local time; the model stores in Z.

## 4. States and enums

- Every entity has a `state` field backed by an explicit enum.
- Enum values are a finite, closed list documented in both the JSON Schema (`enum: [...]`) and the corresponding lifecycle file.
- The **JSON Schema is the source of truth** for enum values. If the lifecycle file disagrees, fix the lifecycle file.
- Nullable enums (e.g., `close_reason` on a Project that is still active) include `null` in the list of allowed values.

## 5. Required vs. optional

- A field is `required` if the entity is invalid without it. Err on the side of *required* — most fields really should be mandatory.
- Optional fields are explicitly allowed `null` when empty, never omitted.
- `additionalProperties: false` on every schema. Unknown fields are rejected. If you need a new field, add it to the schema.

## 6. Soft delete

- Entities that support archival have an `archived_at` timestamp (nullable).
- Archived records **remain** in the dataset. They do not disappear. They are filtered out of live queries but kept for historical reference.
- Hard delete is never the default. Deletion is reserved for exceptional cases (legal requirement, personal data removal request).

## 7. Polymorphic relations

- When an entity can attach to several other kinds of entities (e.g., a Document attached to a Company or a Project), use the pattern:

  ```json
  {
    "entity_type": "project",
    "entity_id": "b2c3d4e5-..."
  }
  ```

- `entity_type` is one of the nine canonical entity slugs: `company`, `brand`, `okr`, `factory`, `project`, `squad`, `task`, `player`, `document`.
- Arrays of polymorphic links are allowed when an entity can attach to many.

## 8. File naming and location

- One JSON Schema per entity, singular: `docs/data-model/schemas/<entity>.schema.json`.
- Test fixtures in `docs/data-model/schemas/_test_fixtures/<entity>.valid.json` and `<entity>.invalid.json`.
- Ontology files: singular entity names under `docs/ontology/<entity>.md`.
- Lifecycle files: singular entity names under `docs/lifecycles/<entity>.md`.
- Keep the triangle consistent: ontology file ↔ lifecycle file ↔ schema file all share the same entity slug.

## 9. Schema `$id` pattern

Every schema's `$id` follows:

```
https://squadflow.dev/schemas/<entity>.json
```

The domain may not resolve today — it is a stable identifier, not a URL that must be fetched. When the framework eventually ships a site, the schemas will be served at these URLs.

## 10. Versioning

- v1.0 schemas are the first public contract. Breaking changes to any field are **forbidden within a major version**.
- Additive changes (new optional fields, new optional enum values) are allowed in minor versions (v1.1, v1.2, …).
- Breaking changes require a major-version bump (v2.0) and a migration guide.

## 11. Cross-language generation

The schemas are designed to generate idiomatic clients in several languages without modification:

```bash
# TypeScript
npx json-schema-to-typescript docs/data-model/schemas/project.schema.json > project.d.ts

# Python (Pydantic)
datamodel-codegen --input docs/data-model/schemas/project.schema.json --output project.py

# Go
# (use quicktype or similar)
```

If a generated client looks wrong, the usual culprit is a schema that violates one of the rules above — a bad enum, a mistyped field, a missing `required`. Fix the schema, not the generated code.

## 12. Validation in CI

Every pull request runs:

1. Meta-schema validation: each file in `schemas/` must validate against JSON Schema draft 2020-12.
2. Fixture validation: the `_test_fixtures/<entity>.valid.json` must validate; the `<entity>.invalid.json` must fail validation.

See [`.github/workflows/lint.yml`](../../.github/workflows/lint.yml) for the exact commands.
