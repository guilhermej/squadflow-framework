# OKR

> An Objective paired with measurable Key Results for a defined period — the bridge between strategy and execution.

OKRs connect direction and work in a single model. The Objective states where you want to be; the Key Results state how you will know if you got there. SquadFlow keeps OKRs as a first-class entity in the same graph as Factories, Projects, and Squads — the contribution is a data edge, not a sentence in a slide.

OKRs are **scoped**: a company-level OKR is sponsored by an Org Steward; a brand-level OKR by the Brand's steward; a squad-level OKR by the Squad Lead. Scope determines who can change it and who owns the score at close.

## Attributes

| Name | Type | Required | Description |
|---|---|---|---|
| `id` | UUID v4 | yes | Canonical identifier. |
| `objective` | string | yes | The direction, in plain language. |
| `key_results` | array of KR | yes | 1–10 Key Results with `name`, `unit`, `baseline`, `target`, and at close `current` and `score`. |
| `period` | string | yes | e.g. `2026-Q2` or `2026`. |
| `commitment` | enum | yes | `committed` or `aspirational`. |
| `owner_id` | UUID (Player) | yes | OKR Sponsor. |
| `company_id` | UUID | yes | Company context. |
| `brand_id` | UUID | no | Brand scope (optional). |
| `squad_id` | UUID | no | Squad scope (optional). |
| `state` | enum | yes | `draft`, `active`, `in_review`, `closed`. |
| `close_outcome` | enum | no | `achieved`, `partially_met`, `missed` — set at close. |
| `score` | number 0.0–1.0 | no | Overall score at close. |
| `contributing_factory_ids`, `_project_ids`, `_squad_ids` | arrays of UUID | no | Contributors. |
| `created_at` / `updated_at` | datetime | yes | Record timestamps. |

Authoritative list: [`../data-model/schemas/okr.schema.json`](../data-model/schemas/).

## Relations

- Sponsored by one **Player** (OKR Sponsor).
- Scoped to one **Company**; optionally to a **Brand** or a **Squad**.
- Contributed to by many **Factories**, **Projects**, and **Squads**.

## Lifecycle and scoring

`draft → active → in_review → closed`. At close, `close_outcome` follows strict thresholds:

| Overall score | Outcome |
|---|---|
| `≥ 0.7` | `achieved` |
| `0.3–0.7` | `partially_met` |
| `< 0.3` | `missed` |

For `committed` OKRs, missing is a real miss — retrospected and accountable. For `aspirational`, missing is expected. See [`../lifecycles/okr.md`](../lifecycles/okr.md).

## Example

*Helios Corp.* sets for 2026 Q2 — Objective: *"Become the preferred billing platform for LATAM SaaS startups."* KRs: active paying customers 420 → 700; MRR 180k → 320k USD; NPS 48 → 65. Sponsored by the CEO, contributed to by the *Sales* Factory, the *Onboarding* Factory, the *Product Onboarding v2* Project, and the *Platform* Squad. At quarter close, the three KR scores (0.33 / 0.25 / 0.35) average to 0.31 — `partially_met`.

## Antipatterns

- **KRs as a to-do list.** KRs are outcomes (*"reduce churn from 6% to 4%"*), not activities (*"launch feature X"*). Activities belong in Projects.
- **Too many OKRs.** 2–5 OKRs per org per period. More is unfocused noise.
- **OKRs without sponsors.** `owner_id` required. "The team" is not a sponsor.
- **Lenient scoring for committed OKRs.** Honest scores or the tool is useless.
