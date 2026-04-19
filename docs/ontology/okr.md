# OKR

> An **OKR** is an Objective paired with measurable Key Results for a defined period — the bridge between strategy and execution in SquadFlow.

## Purpose

OKRs exist so that direction and work are connected in a single model. An Objective states where you want to be ("become the default cybersecurity school in LATAM"). The Key Results state how you will know if you got there ("400k students enrolled", "NPS > 70", "four new certifications launched"). Every Factory, Project, and Squad can truthfully point to at least one OKR it contributes to — or honestly admit it is running on autopilot.

Andy Grove introduced OKRs at Intel in the 1970s; John Doerr took them to Google in 1999. Many frameworks bolt OKRs on as a side tool. SquadFlow keeps them as a **first-class entity in the same graph** as Factories, Projects, and Squads. The contribution relation is a data-model edge, not a bullet point in a Notion page.

OKRs are scoped. A company-level OKR is sponsored by an Org Steward. A brand-level OKR is sponsored by the Brand's steward. A squad-level OKR is sponsored by the Squad Lead. The scope determines who can change it, who reviews it, and who owns the score at the end of the period.

## Attributes

| Name | Type | Required | Description | Example |
|---|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. | `f1a2b3c4-...` |
| `objective` | string | yes | The direction, in plain language. | `Become LATAM's default cybersecurity school` |
| `key_results` | array of KR | yes | 2–5 Key Results, each measurable. | See below |
| `period` | string | yes | Period covered. | `2026-Q2` or `2026` |
| `commitment` | enum | yes | `committed` or `aspirational`. | `committed` |
| `owner_id` | UUID (Player) | yes | OKR Sponsor. | `<player-uuid>` |
| `company_id` | UUID | yes | Company context. | `<company-uuid>` |
| `brand_id` | UUID | no | Brand context (if brand-level). | `null` |
| `squad_id` | UUID | no | Squad context (if squad-level). | `null` |
| `state` | enum | yes | `draft`, `active`, `in_review`, `closed`. | `active` |
| `close_outcome` | enum | no | `achieved`, `partially_met`, `missed`. Set at close. | `null` |
| `score` | number | no | 0.0–1.0 overall score. Set at close. | `null` |
| `created_at` | datetime | yes | Record creation timestamp. | ISO 8601 |
| `updated_at` | datetime | yes | Last modification timestamp. | ISO 8601 |

Each **Key Result** has the shape:

| Field | Type | Description | Example |
|---|---|---|---|
| `name` | string | What is being measured. | `Enrolled students` |
| `unit` | string | Unit of measurement. | `students`, `%`, `USD` |
| `baseline` | number | Value at the start of the period. | `230000` |
| `target` | number | Value at which this KR is achieved. | `400000` |
| `current` | number | Latest measured value. | `265000` |
| `score` | number | 0.0–1.0 contribution to the OKR score. | `0.2` |

The authoritative attribute list is the corresponding JSON Schema at [`../data-model/schemas/okr.schema.json`](../data-model/schemas/).

## Relations

- `OKR` ← sponsored_by ← `Player` (many to 1 — the OKR Sponsor)
- `OKR` ← scoped_to ← `Company` (many to 1, always set)
- `OKR` ← scoped_to ← `Brand` (many to 1, optional)
- `OKR` ← scoped_to ← `Squad` (many to 1, optional)
- `OKR` ← contributed_by ← `Factory` (many to many)
- `OKR` ← contributed_by ← `Project` (many to many)
- `OKR` ← contributed_by ← `Squad` (many to many)

## Lifecycle

States: `draft → active → in_review → closed`. An OKR in `draft` is being shaped; in `active` it is being pursued; in `in_review` the period is ending and the score is being calculated; in `closed` it is scored and filed. At close, `close_outcome` is one of: `achieved` (score ≥ 0.7), `partially_met` (0.3 ≤ score < 0.7), or `missed` (< 0.3).

> See [`../lifecycles/okr.md`](../lifecycles/) for the state diagram and scoring rules.

## Examples

### Example 1 — A company-level quarterly OKR

*Helios Corp.* sets the following OKR for 2026 Q2:

- **Objective:** Become the preferred billing platform for LATAM SaaS startups.
- **Key Results:**
  - Active paying customers: baseline 420, target 700.
  - Monthly recurring revenue: baseline USD 180k, target USD 320k.
  - Net Promoter Score: baseline 48, target 65.

Sponsored by the CEO (`role = org_steward`). Contributed to by the *Sales* Factory, the *Onboarding* Factory, the *Product Onboarding v2* Project, and the *Platform* Squad. Scored at the end of Q2. The `score` is the weighted average of the three KR scores; `close_outcome` follows the thresholds.

### Example 2 — A squad-level aspirational OKR

The *Content* Squad at a multi-brand group sets an aspirational OKR for 2026:

- **Objective:** Make one of our channels the most-watched cybersecurity content source in Brazilian Portuguese.
- **Key Results:**
  - YouTube subscribers across all channels: baseline 180k, target 500k.
  - Average watch time per video: baseline 3:10, target 5:00.
  - Organic newsletter signups per month: baseline 800, target 3000.

`commitment = aspirational` signals that missing is acceptable — the OKR is a stretch, not a contract. Scoring at close follows the same rules, but missed aspirational OKRs do not count against the Squad's performance review.

## Antipatterns

**OKRs as a to-do list.** Key Results are outcomes, not tasks. "Launch feature X" is a task; "reduce churn from 6% to 4%" is a Key Result. If your KR is a binary checkbox, it is probably a Project, not a KR.

**Too many OKRs.** If every department has three OKRs and every squad has three OKRs, nothing is prioritized. A healthy company has 2–5 OKRs total per period, not per team.

**OKRs without sponsors.** An OKR without a single accountable person drifts. `owner_id` is required. "The team" is not a sponsor.

**Committed OKRs graded leniently.** If you set a committed OKR and missed, that is a real miss — not a "we got close". The score is honest, the learning is in the retrospective. Ducking accountability destroys the tool.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Roles (OKR Sponsor): [`../processes/roles.md`](../processes/)
- Lifecycle: [`../lifecycles/okr.md`](../lifecycles/)
- Schema: [`../data-model/schemas/okr.schema.json`](../data-model/schemas/)
- Related entities: [Company](company.md), [Brand](brand.md), [Factory](factory.md), [Project](project.md), [Squad](squad.md)
