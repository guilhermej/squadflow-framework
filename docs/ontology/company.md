# Company

> A **Company** is a legal entity with a single tax identity that employs people, owns brands, runs factories, and sponsors projects and OKRs.

## Purpose

A Company is the outermost container in SquadFlow. It represents the *legal person* — the LLC, the Ltda, the GmbH, the corp — that signs contracts, pays taxes, and holds employment relationships. Everything else in the framework ultimately sits under one Company.

A Company is distinct from a **Brand**. A Company is the *legal* identity (registered name, tax ID); a Brand is the *commercial* identity (the name you market to customers). A Company can carry many Brands, and a Brand can rarely span more than one Company. Keeping them separate is the first discipline SquadFlow asks of you.

Most small companies run with a single Brand that shares the Company's name. That is fine. You still create one Company and one Brand, because the moment you add a second product line, sister company, or acquisition, the two concepts will drift apart.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `a1b2c3d4-...` |
| `name` | string | yes | Common name used in conversation. | `Guardsi` |
| `legal_name` | string | yes | Official registered name. | `Guardsi Tecnologia LTDA` |
| `tax_id` | string | yes | Primary tax identifier (CNPJ, EIN, UTR…). | `23.353.677/0001-09` |
| `jurisdiction` | string | yes | ISO country code + region, e.g. `BR-SP`. | `BR-SP` |
| `state` | enum | yes | `active` or `archived`. | `active` |
| `founded_on` | date | no | Incorporation date. | `2016-03-15` |
| `archived_on` | date | no | Set when `state` becomes `archived`. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/company.schema.json`](../data-model/schemas/). If this table and the schema disagree, the schema wins — fix the file.

## Relations

- `Company` → owns → `Brand` (1 to many)
- `Company` → employs → `Player` (1 to many)
- `Company` → runs → `Factory` (1 to many)
- `Company` → sponsors → `OKR` (1 to many — company-level OKRs)
- `Company` → scopes → `Project` (1 to many, when not scoped to a specific Brand)

## Lifecycle

Trivial: `active → archived`. A Company is archived only when it is legally dissolved, merged, or sold. Archive is soft — historical records remain linked.

> See [`../lifecycles/company.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — Single-company startup

*Helios SaaS* is a small B2B startup with one legal entity (*Helios Corp., Delaware LLC*) and one brand (*Helios*, the product name). Ana, the founder, creates one Company record with `name = "Helios"`, `legal_name = "Helios Corp."`, `tax_id = EIN-...`, and one Brand record (next file). For her, the two records are near-duplicates. That's fine — keeping them separate costs nothing and pays off the day she launches a second product.

### Example 2 — Multi-company group

Grupo Solyd runs two Companies: *Guardsi Tecnologia LTDA* (B2B cybersecurity services and education) and *Mindz LTDA* (SaaS platforms for infoproduct businesses). Each is a separate legal entity with its own CNPJ. Players are employed by one Company or the other. Factories and Projects hang off whichever Company legally owns the work. Brands — *Solyd*, *Guardsi*, *Mindz*, *Caveiratech*, *Solyd Hunter* — attach to the Company that legally supports them, even when they share office space and leadership.

## Antipatterns

**Collapsing Company and Brand into one record.** Tempting when you only have one of each. Do not do it. The day you add a second brand, a second legal entity, or an acquisition, the ontology breaks and migration is painful.

**Using Company as a folder.** A Company is not a Notion workspace or a tag. It is a legal entity. Do not create a Company record just to group unrelated work — use Squads or Documents for that.

**Archiving a Company to hide work.** If a business line is shutting down, archive the Factories and Projects, not the Company. Archiving the Company should only reflect real legal dissolution.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Lifecycle: [`../lifecycles/company.md`](../lifecycles/)
- Schema: [`../data-model/schemas/company.schema.json`](../data-model/schemas/)
- Related entities: [Brand](brand.md), [Player](player.md), [Factory](factory.md)
