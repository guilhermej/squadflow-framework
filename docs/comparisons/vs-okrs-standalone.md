# SquadFlow vs. OKRs alone

## TL;DR

OKRs (Objectives and Key Results) are a goal-setting discipline. Used alone, they tell you *what* you are trying to achieve but say nothing about *how* your teams, kanbans, and cadences organize themselves to get there. SquadFlow keeps OKRs as a first-class entity and wraps a full operational frame around them — Factories, Projects, Squads, and governance — so that the goals connect to real work.

## What OKRs do well

- **Simple and memorable.** Every organization can learn the format in five minutes.
- **Forcing function for clarity.** Writing an Objective and 2–4 Key Results forces teams to articulate what they are actually trying to do.
- **Language-independent.** OKRs are a method, not a tool; they translate across cultures and industries.
- **Decades of validation.** From Intel in the 1970s (Andy Grove) to Google in 1999 (John Doerr) to thousands of companies since.
- **Sponsor-accountable.** Each OKR has a named owner, avoiding committee-driven fuzziness.

## Where OKRs alone fall short

- **No operational frame.** OKRs say nothing about how work gets organized into teams, queues, and cadences. Companies running OKRs often realize they still need a team structure, a sprint rhythm, a backlog, and governance — and have to pull those from elsewhere.
- **Connection to work is fragile.** The gap between an OKR and a Jira ticket is rarely formal. People *claim* their work supports an OKR without having to prove it.
- **Ceremony gaps.** OKRs have a setting event and a scoring event. They do not prescribe weekly alignment, daily debriefings, or continuous review — all of which real organizations need.
- **Easily gamed.** Without governance, a team can set soft KRs, score them generously, and look great on paper while the business stagnates.
- **Continuous work invisible.** OKRs optimize for outcomes. Operational work that maintains outcomes (support, onboarding, billing) does not fit neatly — it becomes either an OKR tacked-on ("maintain NPS above 60") or invisible to leadership.

## What SquadFlow adds

- **OKRs remain first-class.** Nothing is taken away.
- **Factories and Projects** make the rest of the work visible and governed.
- **Formal contribution links** between OKRs and the work that supports them (`contributed_by` relation). A Factory or Project that cannot name the OKR it serves has a legible problem.
- **Ceremonies for OKR hygiene.** OKR Setting and Review are named, scheduled, and bracketed by Portfolio Review and Strategic Cadence.
- **Scoring rules** — not just a number, but an outcome tier (`achieved` / `partially_met` / `missed`) that is preserved and retrospected.
- **Governance** that distinguishes `committed` OKRs (where misses are accountable) from `aspirational` (where stretch is expected).

## Side-by-side

| Dimension | OKRs alone | SquadFlow |
|---|---|---|
| Strategy layer | OKRs only | OKRs + formal contribution links |
| Execution layer | Not modeled | Factories + Projects + Squads + Tasks |
| Cadence | Quarterly set/review | Daily → yearly stack |
| Governance | Implied | RACI matrix + decision logs |
| Continuous ops | Invisible | Factories (first-class) |
| Data model | Informal | JSON Schema per entity |
| Risk of theatre | High (no link to work) | Low (work is in the graph) |

## When to use OKRs alone

- You are a small team (< 10 people) and OKRs plus common sense are all you need. Adding a framework is overhead.
- Your organization already has a working operational structure (it's inherited, it just works) and all you need is the goal-setting layer on top.
- You are an advisor or consultant who wants to introduce OKRs to a client without overhauling their operating system. Keep it minimal.

## Adopting SquadFlow if you already use OKRs

If your organization uses OKRs well and you want to grow the rest of the operating system:

1. **Keep your OKRs as they are.** Create the OKR records in SquadFlow; link each to a Company, Brand, or Squad as appropriate.
2. **Catalog your work into Factories and Projects.** Every Factory and Project must link to at least one OKR (except pure maintenance work, which can be explicit about having no OKR link).
3. **Define Squads.** Map each OKR to the Squads contributing. If an OKR has no Squad working on it, it is at risk.
4. **Add the operational cadence.** Weekly Squad Sync and Factory Review run on top of the quarterly OKR rhythm you already have.
5. **Introduce governance.** Document who approves what — the RACI matrix in [governance.md](../processes/governance.md) is a starting point.

The common trap is adding every SquadFlow element at once. Do not. Add Factories first, then Squads, then the weekly cadence, then the rest. Each step should feel like filling an obvious gap, not like bureaucracy.

## A common symptom

A classic sign an organization has outgrown OKRs-only: *"We set OKRs every quarter and score them, but between setting and scoring nothing really changes. People work on what they were already working on."* This is an execution-layer problem, not an OKR problem. SquadFlow's factories-and-projects layer is designed to fix that gap.

## See also

- [OKR ontology](../ontology/okr.md)
- [OKR lifecycle](../lifecycles/okr.md)
- [Measure What Matters](https://www.whatmatters.com/) — John Doerr's book, the standard reference for OKRs.
- [Manifesto](../../MANIFESTO.md)
