# Governance

Governance in SquadFlow answers a single question: **who approves what**. The answer is a small RACI matrix, four principles, and a decision-log pattern. Nothing more.

## Four principles

### 1. Every entity has a single owner.

Never a committee. Every Factory, Project, Squad, OKR, and Document has exactly one accountable Player. Shared accountability is unowned accountability.

### 2. Approvals are logged.

Any approval that changes a sensitive state — retiring a Factory, absorbing a Project, dissolving a Squad, setting or closing a company OKR — creates a decision-log entry. The entry records who approved, when, and why. The log lives attached to the entity (as a Document, a page, or a native property depending on your tooling).

### 3. Stewards do not micromanage.

Org Stewards approve transitions of state, not Tasks. A Steward who approves every Task is doing Squad Lead work. A Steward who approves nothing is doing rubber-stamp work.

### 4. Roles are not titles.

SquadFlow governance names Roles (Squad Lead, Factory Manager, OKR Sponsor, Org Steward), not people or job titles. This keeps governance working when people change jobs and the organization changes shape. See [roles.md](roles.md).

## RACI summary

| Action | Approver(s) | Convened at |
|---|---|---|
| Create Company | Org Steward | ad-hoc |
| Archive Company | Org Steward | ad-hoc |
| Create Brand | Org Steward | ad-hoc |
| Archive Brand | Org Steward | ad-hoc |
| Create Factory | Org Steward | Portfolio Review or ad-hoc |
| Retire Factory | Org Steward + Factory Manager | Factory Retirement Review |
| Create Project | Project Owner (+ OKR Sponsor if OKR-linked) | Portfolio Review or ad-hoc |
| Approve Project scope | Project Owner + Org Steward | during `scoping` |
| Start Project | Squad Lead + Project Owner | Project Kickoff |
| Cancel Project | Project Owner + Org Steward | ad-hoc |
| Close Project (delivered) | Project Owner | Project Closing |
| Absorb Project (into Factory) | Project Owner + Org Steward | Project Closing |
| Form Squad | Squad Lead + Org Steward | Squad Formation |
| Pause Squad | Squad Lead + Org Steward | ad-hoc |
| Dissolve Squad | Squad Lead + Org Steward | Squad Dissolution Handoff |
| Define OKR (company / brand) | OKR Sponsor | OKR Setting |
| Define OKR (squad-level) | OKR Sponsor | OKR Setting |
| Close and score OKR | OKR Sponsor | OKR Review |
| Onboard Player | HR + Org Steward | ad-hoc |
| Offboard Player | HR + Org Steward | ad-hoc |
| Publish Document | Owner (after `in_review` approval) | ad-hoc |
| Flag Document as `outdated` | Any Player | ad-hoc |
| Archive Document | Owner + Steward | ad-hoc |
| Assign a Task | Squad Lead, Factory Manager, or Project Owner | Squad Sync or kanban edit |
| Cancel a Task | Assignee, or the parent's Owner | ad-hoc |

## The decision-log pattern

Sensitive transitions are not only *approved*; they are *explained*. A decision log is a short dated record attached to the affected entity, with three fields:

| Field | Purpose |
|---|---|
| **Decision** | One sentence — what was decided. |
| **Rationale** | 1–3 sentences — why. Reference the alternatives considered. |
| **Approved by** | The Role(s) that approved. |

An example attached to a Project at close:

> **2026-07-12 — Absorb into new Factory**
>
> Absorbed into the new *Partner Operations* Factory. The ongoing operational load (contract renewals, commission calculations, partner onboarding) will not self-sustain without dedicated owners, and the alternatives (hand off to *Go-to-Market* Squad ad-hoc; automate fully) were judged too brittle for the volume expected in H2.
>
> Approved by: Project Owner (Ana Silva) + Org Steward (Guilherme Junqueira Soares)

The log may live as a Document, a Notion page, a section of the entity's page, or a structured column in a future system — the point is that it is **retrievable later**, not the specific medium.

## Anti-decisions

Some actions need no approval beyond the individual doing the work. Examples:

- Creating a Task on a Factory you manage.
- Starting or completing a Task assigned to you.
- Flagging a Document `outdated`.
- Moving a kanban card to the next stage in a Factory.

If you find yourself requiring approval for these, your governance has slipped into theatre.

## Disagreements

When two approvers disagree (e.g., Squad Lead wants to pause the Squad, Org Steward wants to dissolve it), the higher-scoped Role decides — Org Steward over Squad Lead, OKR Sponsor over Project Owner for OKR-aligned work. The decision log records the disagreement and its resolution. Overrides are acceptable; silent overrides are not.

## See also

- [Roles](roles.md) — who each approver is.
- [Lifecycles](../lifecycles/) — where each transition is triggered.
- [Ceremonies](ceremonies.md) — where most decisions are made.
- [Manifesto](../../MANIFESTO.md) — principle 2 ("every entity has a single owner") and principle 3 ("states are explicit").
