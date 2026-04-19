# Cadences

The **cadence stack** is the rhythm at which the organization looks at its work. SquadFlow defines cadences from daily to yearly; each one has a clear purpose, a Role that convenes, and a defined output.

The stack is opinionated. You can skip a level if your organization does not need it (a 20-person company usually skips monthly Portfolio Review). You cannot invert a level — weekly work is not reviewed monthly in SquadFlow.

## The stack

| Frequency | Ceremony | Scope | Duration | Convened by |
|---|---|---|---|---|
| Daily | [Debriefing](ceremonies.md#debriefing) | all Players | ≤ 15 min async or live | Squad Lead |
| Weekly | [Squad Sync](ceremonies.md#squad-sync) | per Squad | ~30 min | Squad Lead |
| Weekly | [Factory Review](ceremonies.md#factory-review) | per Factory | ~30 min | Factory Manager |
| Monthly | [Portfolio Review](ceremonies.md#portfolio-review) | Stewards + Leads | ~60 min | Org Steward |
| Quarterly | [OKR Setting / Review](ceremonies.md#okr-setting-and-review) | org-wide | ~90 min per session | OKR Sponsors + Org Steward |
| Quarterly | [Strategic Cadence](ceremonies.md#strategic-cadence) | Org Stewards | ~120 min | Org Steward |
| Yearly | Annual Planning + Annual OKRs | org-wide | full day | Org Steward |

## Ad-hoc cadence

Some cadences are **triggered by lifecycle transitions**, not the calendar:

| Trigger | Ceremony |
|---|---|
| Project `scoping → active` | Project Kickoff |
| Project `active/delivery → closed` | Project Closing / Retrospective |
| Squad `forming → active` | Squad Formation |
| Squad `active → dissolving` | Squad Dissolution Handoff |
| Factory `active → retired` | Factory Retirement Review |

See [ceremonies.md](ceremonies.md) for the purpose, attendees, and outputs of each.

## Design principles

**Symmetry between continuous and change work.** Factories have a weekly Review because the work is continuous. Projects have a Kickoff and a Closing because the work is bounded. SquadFlow refuses to force one shape onto both.

**Shortest useful interval.** Daily debriefings for Player-level coordination. Weekly for Squad-level coordination. Quarterly for strategic direction. If you feel you need a new cadence, first check whether an existing one can absorb the need.

**Every cadence has a Role that convenes.** Cadences do not self-organize. If a Role is vacant, the cadence does not run. A Squad without a Lead has no Squad Sync.

**Every cadence has an output.** If a meeting exists and produces nothing that anyone references afterward, it is a waste. See each ceremony's definition for its specific output.

## How to add a new cadence

Do not add new cadences lightly. The default answer is no. If you believe a new cadence is truly needed:

1. Open an Issue describing the gap the existing cadences leave.
2. Propose the new ceremony: purpose, frequency, duration, Role, attendees, inputs, outputs, antipatterns.
3. If accepted, add it to [ceremonies.md](ceremonies.md) and update this stack.

## See also

- [Ceremonies](ceremonies.md) — the full catalog.
- [Roles](roles.md) — who convenes each ceremony.
- [Governance](governance.md) — decisions that happen at each cadence.
