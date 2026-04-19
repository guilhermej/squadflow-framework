# Roles

Named responsibilities held by Players. One Player can hold several Roles. Roles are not job titles, not compensation tiers, and not HR reporting lines.

SquadFlow v1.0 has **six canonical Roles**. Every approval in the framework names a Role, not a person — so governance survives people changing jobs.

## The six Roles

| Role | Scope | Responsibility | Held by |
|---|---|---|---|
| **Player** | individual | Executes Tasks; participates in Squad ceremonies; surfaces blockers. | Every Player by default. |
| **Squad Lead** | 1 Squad | Coordinates the Squad; ensures cadence runs (Sync, Debriefing); surfaces Squad-level impediments. | One Player per Squad. Mandatory. |
| **Factory Manager** | 1 Factory | Owns the kanban — stages, throughput, manual. Runs the weekly Factory Review. Decides what enters the board. | One Player per Factory. Mandatory. |
| **Project Owner** | 1 Project | Accountable for the Project's delivery. Owns scope, timeline, close decision. | One Player per Project once in `scoping` or later. |
| **OKR Sponsor** | N OKRs | Shapes the Objective, defines KRs, commits, defends, scores at close. | Typically Org Steward (company/brand OKRs) or Squad Lead (squad OKRs). |
| **Org Steward** | 1 Company / Brand | Overall health of the entity. Approves state transitions (create/retire Factory, cancel/absorb Project, dissolve Squad). Does **not** micromanage. | Typically a founder, CEO, COO, or GM. |

## Signals and antipatterns

- **Squad Lead** — Cadence is consistent and useful; work is either accepted deliberately or declined explicitly. *Antipattern:* empty hat with no visible coordination, or tech-leading every Task.
- **Factory Manager** — Factory Review is crisp; throughput metrics are visible; operating manual is current. *Antipattern:* running the Factory without a Review.
- **Project Owner** — Scope is clear and stable; close decision is explicit. *Antipattern:* letting scope creep silently; delaying close indefinitely.
- **OKR Sponsor** — Objective is unambiguous; KRs are outcomes not activities; scoring at close is honest. *Antipattern:* KRs as a to-do list; lenient scoring for committed OKRs.
- **Org Steward** — Transitions happen deliberately with decision logs; portfolio stays aligned with strategy. *Antipattern:* approving every Task (micromanagement) or approving nothing (rubber-stamp).

## How Roles stack

One Player, several Roles:

- A founder in a small company: `org_steward` + `okr_sponsor` + `factory_manager` for one key Factory.
- A senior engineer: `player` + `squad_lead` + `project_owner` for a specific Project.
- A COO of a multi-brand group: `org_steward` for the Company + `okr_sponsor` for company OKRs; brand-level stewardship delegated elsewhere.

Roles are encoded in the Player's `role_slugs` attribute.

## Roles versus job titles

- *Senior Backend Engineer* is a **job title**. Not a SquadFlow concept.
- *Squad Lead* is a **Role**. Independent of title, compensation, or reporting.

Promotions, compensation, and org-chart reporting live outside the ontology.

## See also

- [Player ontology](../ontology/player.md) — the `role_slugs` attribute.
- [Governance](governance.md) — which Role approves what.
- [Ceremonies](ceremonies.md) — which Role convenes each ceremony.
