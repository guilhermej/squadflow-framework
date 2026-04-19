# Company

> A legal entity — the LLC/Ltda/Corp that signs contracts, pays taxes, and employs Players.

A Company is the outermost container in SquadFlow. It is the *legal* identity; a Brand is the *commercial* identity. A single Company can carry many Brands, and a Brand rarely spans more than one Company. Most small companies run with a single Brand that shares the Company's name — fine, but keep the two records separate, because the day you add a second brand or legal entity, the two concepts diverge and migrating later is painful.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `name` | string | yes | Common name. |
| `legal_name` | string | yes | Registered name (e.g. "Guardsi Tecnologia LTDA"). |
| `tax_id` | string | yes | Primary tax identifier (CNPJ, EIN, UTR…). |
| `jurisdiction` | string | yes | ISO country code + region (e.g. `BR-SP`). |
| `state` | enum | yes | `active` or `archived`. |
| `founded_on` | date | no | Incorporation date. |
| `archived_on` | date | no | Set when archived. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/company.schema.json`](../data-model/schemas/).

## Relations

- Owns one or many **Brands**.
- Employs one or many **Players**.
- Runs one or many **Factories**.
- Scopes **OKRs** (company-level) and **Projects** (when not brand-scoped).

## Lifecycle

`active → archived`. Archive only on legal dissolution, merger, or sale — never to hide work. See [`../lifecycles/company.md`](../lifecycles/company.md).

## Example

Grupo Solyd runs two Companies: *Guardsi Tecnologia LTDA* (cybersecurity services and education) and *Mindz LTDA* (SaaS platforms). Each has its own CNPJ, payroll, and contracts. Brands like *Solyd*, *Guardsi*, *Mindz*, *Caveiratech*, and *Solyd Hunter* attach to the Company that legally supports them.

## Antipatterns

- **Collapsing Company and Brand into one record.** Costs nothing to keep separate now; costs a lot to split later.
- **Using Company as a folder.** A Company is a legal entity, not a tag or workspace.
- **Archiving a Company to hide work.** Archive the work (Factories, Projects) instead; archive the Company only on actual dissolution.
