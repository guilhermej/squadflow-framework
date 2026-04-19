# Brand

> A **Brand** is a commercial identity — a market-facing name, voice, and product line — owned by one or more Companies.

## Purpose

A Brand is the face the market sees. Customers buy *Helios*, not *Helios Corp.*. Students enroll in *Solyd*, not *Guardsi Tecnologia LTDA*. Keeping the commercial identity separate from the legal identity lets you run a single business under multiple brands, or spin up a new brand without creating a new company, or sell a brand without selling the company that birthed it.

A Brand is distinct from a **product**. A brand can carry many products under its umbrella — *Solyd* the brand carries *Solyd One* the product, *Solyd Hunter* the program, and other content lines. Products are not a first-class entity in SquadFlow v1.0; they live inside the Brand record or as Documents.

A Brand is almost always owned by one Company. Edge cases exist — joint ventures, licensing arrangements — where a Brand spans multiple Companies. The schema allows it, but you should pause and check whether that is actually true for your business before modeling it that way.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `b1c2d3e4-...` |
| `name` | string | yes | Commercial name. | `Solyd` |
| `company_ids` | array of UUID | yes | Owning Company (usually exactly one). | `["a1b2c3..."]` |
| `tagline` | string | no | Short market-facing slogan. | `The largest cybersecurity school in LATAM` |
| `website` | string (URL) | no | Primary marketing site. | `https://solyd.com.br` |
| `state` | enum | yes | `active` or `archived`. | `active` |
| `launched_on` | date | no | Date the brand went public. | `2015-01-10` |
| `archived_on` | date | no | Set when `state` becomes `archived`. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/brand.schema.json`](../data-model/schemas/).

## Relations

- `Brand` ← owned_by ← `Company` (many to 1 — usually exactly 1)
- `Brand` → scopes → `Project` (1 to many)
- `Brand` → carries → `Factory` (1 to many, optional — some factories are brand-scoped, some are company-scoped)
- `Brand` → sponsors → `OKR` (1 to many — brand-level OKRs)

## Lifecycle

Trivial: `active → archived`. A Brand is archived when it is sunset — the market no longer sees it. Archive is soft; historical Factories and Projects stay linked.

> See [`../lifecycles/brand.md`](../lifecycles/) for the state diagram.

## Examples

### Example 1 — One company, one brand

*Helios SaaS* runs one Brand (`Helios`) under one Company (`Helios Corp.`). The Brand and Company records share most fields. When *Helios* launches a sister product line called *Helios Labs* two years later, Ana creates a second Brand record under the same Company — no new legal entity needed.

### Example 2 — One company, multiple brands

*Guardsi Tecnologia LTDA* (Company) carries at least four Brands:

- **Solyd** — a cybersecurity education platform (students, courses, certifications).
- **Guardsi** — B2B services (pentest, phishing simulations, OSINT, awareness training).
- **Caveiratech** — media and content (YouTube channel, Instagram, newsletter).
- **Solyd Hunter** — a program connecting Solyd students to pentest opportunities.

Each Brand has its own tagline, website, and content voice, but payroll, contracts, and taxes run through the single Company record. When a Project is scoped to *Guardsi* specifically, it sets `brand_id = <Guardsi's id>`. When a Project is cross-brand, it sets `company_id` and leaves `brand_id` null.

## Antipatterns

**Creating one Brand per product line.** Product lines belong inside a Brand. If your customers perceive *Helios* and *Helios Labs* as the same brand with two product tiers, model it as one Brand. Only split if the market genuinely sees two different brands.

**Brands without an owning Company.** A Brand cannot exist without a legal entity to support it. `company_ids` is required.

**Using Brand as a squad grouping.** Squads are not owned by Brands — they are owned by Companies. A single Squad can serve multiple Brands. Do not duplicate Squads per Brand.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Lifecycle: [`../lifecycles/brand.md`](../lifecycles/)
- Schema: [`../data-model/schemas/brand.schema.json`](../data-model/schemas/)
- Related entities: [Company](company.md), [Project](project.md), [OKR](okr.md)
