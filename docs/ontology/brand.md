# Brand

> A commercial identity — a market-facing name, voice, and product line — owned by one or more Companies.

A Brand is the face the market sees. Customers buy *Solyd*, not *Guardsi Tecnologia LTDA*. Keeping commercial identity separate from legal identity lets you run multiple Brands under one Company, spin up a new Brand without a new company, or sell a Brand without selling its parent. A Brand is distinct from a product: a Brand can carry many products; products are not first-class in SquadFlow v1.0.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `name` | string | yes | Commercial name. |
| `company_ids` | array of UUID | yes | Owning Company (usually exactly one). |
| `tagline` | string | no | Short market-facing slogan. |
| `website` | string (URL) | no | Primary marketing site. |
| `state` | enum | yes | `active` or `archived`. |
| `launched_on` | date | no | Public launch date. |
| `archived_on` | date | no | Set when sunset. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/brand.schema.json`](../data-model/schemas/).

## Relations

- Owned by one or more **Companies**.
- Scopes **Projects**, **OKRs**, and sometimes **Factories**.

## Lifecycle

`active → archived`. Archive when the Brand is sunset. See [`../lifecycles/brand.md`](../lifecycles/brand.md).

## Example

*Guardsi Tecnologia LTDA* (Company) carries four Brands: **Solyd** (cybersecurity education), **Guardsi** (B2B pentest services), **Caveiratech** (media), and **Solyd Hunter** (talent program). Each has its own tagline, website, and voice; payroll and contracts all run through the single Company.

## Antipatterns

- **One Brand per product line.** Product lines belong inside a Brand. Split only when the market genuinely sees two brands.
- **Brands without an owning Company.** A Brand always has a legal home.
- **Using Brand to group Squads.** Squads are owned by Companies; a single Squad can serve multiple Brands.
