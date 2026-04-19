# Roles

A **Role** is a named responsibility. Roles are held by Players. One Player can hold several Roles at once. Roles are not job titles and are not compensation tiers.

SquadFlow v1.0 has **six canonical Roles**. Every approval in the framework names a Role, not a person, so the system survives people changing jobs and the organization changing shape.

## The six Roles

### Player

**Scope:** individual.

**Responsibility:** execute Tasks assigned to them, participate in Squad ceremonies, surface blockers.

**Held by:** every Player in the organization, by default.

**Signals of doing this well:** Tasks completed on schedule, blockers surfaced early, active participation in Squad Sync and Debriefing.

**Antipatterns:** treating a Player as a ticket factory (no ownership), or treating them as a cost center (not a contributor).

---

### Squad Lead

**Scope:** one Squad.

**Responsibility:** coordinates the Squad, ensures cadence (Squad Sync, Debriefing, handoffs) happens, surfaces Squad-level impediments to the Org Steward, proposes new Factories or Projects the Squad should take on.

**Held by:** one Player per Squad. Mandatory.

**Signals of doing this well:** Squad Sync is consistent and useful; members know what they are working on and why; new work is either accepted deliberately or declined explicitly.

**Antipatterns:** becoming a tech lead on every Task (micromanagement); being an empty hat with no visible coordination.

---

### Factory Manager

**Scope:** one Factory.

**Responsibility:** owns the kanban — its stages, its throughput, its documentation. Runs the weekly Factory Review. Proposes improvements (often as new Projects). Has final say on what enters the kanban.

**Held by:** one Player per Factory. Mandatory.

**Signals of doing this well:** the Factory Review is crisp and surface-able; throughput metrics are visible; the operating manual is current; stuck cards are rare.

**Antipatterns:** running the Factory without a Review (invisible work); accepting every card (no filter); failing to retire stages that are no longer useful.

---

### Project Owner

**Scope:** one Project, for the duration of the Project.

**Responsibility:** accountable for the Project's delivery. Owns the scope, negotiates the timeline, decides cancellation or absorption, records the decision log, runs the Kickoff and Closing ceremonies.

**Held by:** one Player per Project. Mandatory for Projects in `scoping` or later states.

**Signals of doing this well:** scope is clear and stable; weekly status is honest (not color-coded lies); `delivery` happens on schedule and cleanly; close decision is explicit.

**Antipatterns:** letting scope creep silently; delaying the close decision indefinitely; absorbing a Project without creating a Factory.

---

### OKR Sponsor

**Scope:** one or more OKRs.

**Responsibility:** shapes the Objective, defines the Key Results, commits the OKR, defends it throughout the period, scores it at close. Keeps the OKR honest — does not game the score.

**Held by:** typically an Org Steward (for company or brand OKRs) or a Squad Lead (for squad OKRs). One Sponsor per OKR.

**Signals of doing this well:** the Objective is unambiguous; KRs are outcomes, not activities; scoring at close is honest; missed OKRs are retrospected.

**Antipatterns:** KRs as a to-do list; lenient scoring for committed OKRs; dozens of OKRs instead of a focused few.

---

### Org Steward

**Scope:** one Company or one Brand.

**Responsibility:** overall health of the entity. Approves creation and retirement of Factories, cancellation or absorption of Projects, formation and dissolution of Squads. Sponsors company- or brand-level OKRs. Does **not** micromanage — approves transitions of state, not Tasks.

**Held by:** typically a founder, CEO, COO, or a GM for brand-level stewardship. One Steward per Company (or per Brand, when brand-level stewardship is delegated).

**Signals of doing this well:** transitions happen deliberately and with decision logs; the portfolio of Factories and Projects stays aligned with strategy; Squad Leads and Factory Managers escalate freely.

**Antipatterns:** approving every Task (micromanagement); approving nothing (rubber-stamp); letting stale Factories or zombie Projects linger.

## How Roles stack

One Player can hold several Roles. Examples:

- A founder in a small company: `org_steward` + `okr_sponsor` + `factory_manager` for a sales factory.
- A senior engineer: `player` + `squad_lead` + `project_owner` for a migration Project.
- A COO of a multi-brand group: `org_steward` (company-wide) + `okr_sponsor` for the company OKRs + Brand Stewardship delegated elsewhere.

Roles are encoded in the Player's `role_slugs` attribute (see [`../ontology/player.md`](../ontology/player.md)).

## Roles versus job titles

- *Senior Backend Engineer* is a **job title**. Not a SquadFlow concept.
- *Player* is a **Role** in SquadFlow. Often held by people with engineering titles, but the two are independent.

Promotions, compensation, and HR reporting structures live outside the ontology. SquadFlow cares only which Roles a Player currently holds.

## See also

- [Player entity](../ontology/player.md) — the `role_slugs` attribute.
- [Governance](governance.md) — which Role approves what.
- [Ceremonies](ceremonies.md) — which Role convenes each ceremony.
