# SquadFlow vs. SAFe

## TL;DR

SAFe (Scaled Agile Framework) is the dominant heavyweight enterprise-scale framework. It describes how dozens or hundreds of teams coordinate across a large organization using multi-week ceremonies and many roles. SAFe works where the problem is truly enterprise-scale and there is capacity to fund certification, coaches, and ceremony. SquadFlow is deliberately smaller and open — aimed at 10–200-person scale-ups and multi-brand groups that would choke on SAFe.

## What SAFe does well

- **Real enterprise scale.** SAFe has been deployed in organizations with thousands of engineers. Nothing in SquadFlow has been tested at that size.
- **Program Increment (PI) Planning.** A synchronized 2-day event where all teams in a release train align. Polarizing, but real teams report it works.
- **Prescriptive answers to hard coordination problems.** Lean Portfolio Management, Agile Release Trains, Value Streams, Solution Trains. When you need this much coordination, SAFe has an opinion.
- **A coach and certification network.** If you hire a SAFe coach, they can implement the framework faithfully. Implementation partners, training tracks, certifications at many levels.

## Where SAFe is limited

- **Heavy.** Many roles (RTE, PM, PO, Business Owner, Epic Owner, System Architect, Solution Architect…). Many artifacts. Many ceremonies. The overhead is real, and it is *not* something a 50-person company should adopt.
- **Expensive.** Certifications and coaching are paid products. Adopting SAFe as a company costs five to seven figures a year in training, coaching, and tooling.
- **Closed.** The framework is proprietary. You can reference it, but you cannot adapt and redistribute it. Derivative works are restricted.
- **Change-work bias.** SAFe is primarily oriented toward delivering features across release trains. Continuous operations (sales, support, content, billing) live at the edges.
- **Complexity tax.** Every company using SAFe spends measurable energy on the framework itself. In large enterprises this is a rounding error. In 100-person companies it is a significant portion of leadership capacity.

## What SquadFlow adds — or removes

Compared to SAFe, SquadFlow is **intentionally smaller**:

- **9 entities** instead of ~25.
- **6 Roles** instead of ~15.
- **4 process files** (roles, cadences, ceremonies, governance) instead of hundreds of pages.
- **Open (CC-BY-SA 4.0)** instead of proprietary.
- **Continuous ops native** via Factories instead of buried in Kanban boards under the release train.
- **One formal data model** instead of Confluence pages describing artifacts.

SAFe adds features; SquadFlow subtracts them.

## Side-by-side

| Dimension | SAFe | SquadFlow |
|---|---|---|
| Target size | 100s–1000s of people | 10–200 people |
| Entities / roles | ~25 / ~15 | 9 / 6 |
| Cadence | PI Planning, System Demo, Inspect & Adapt, etc. | Daily → quarterly stack |
| Continuous ops | Peripheral | First-class (Factories) |
| License | Proprietary | CC-BY-SA 4.0 |
| Cost | Certifications, coaches, tooling | Zero |
| Data model | Informal | JSON Schemas per entity |
| Adoption bar | High (training, coaches) | Low (read a repo) |

## When to pick SAFe instead

- You are running **500+ engineers** across multiple release trains, and the problem is genuinely enterprise-scale coordination.
- Your organization has **committed budget** for certification and coaching and will complete it.
- You need the **prescriptiveness** — your org needs a framework that tells it exactly what to do, not one that expects you to think.
- You value **vendor support** (training, certification, coaches) over open-source adaptability.

## When to pick SquadFlow instead

- You are a **scale-up** (10–200 people) and SAFe is obvious overkill.
- You run **multiple brands or business units** and want a single ontology across them.
- You value **openness** — you want to adapt, translate, or build on the framework.
- You want a **data model** as a first-class artifact, not a training deck.

## Migrating from SAFe to SquadFlow

If your organization is shrinking out of SAFe (too heavy for your current scale) or never was enterprise-enough to need it:

1. **Compress roles.** RTE → Squad Lead. PM → Project Owner. PO → Factory Manager (for operational backlogs) or Project Owner (for change). Business Owner / Epic Owner → Org Steward or OKR Sponsor.
2. **Collapse release trains into Squads.** A release train at SAFe scale is multiple Squads in SquadFlow; at smaller scale, it is one Squad.
3. **Re-home continuous ops.** Any work that was flowing through release trains but is actually continuous becomes a Factory.
4. **Keep PI Planning if it works.** Rename it to "Quarterly OKR Setting + Strategic Cadence". Same event, smaller guest list.
5. **Drop what you were doing for SAFe compliance.** Any ceremony that existed only to satisfy the framework — not the work — stops.
6. **Write decision logs.** SAFe's reliance on process becomes SquadFlow's reliance on explicit, dated decisions.

## See also

- [Manifesto](../../MANIFESTO.md)
- [Governance](../processes/governance.md)
- [Scaled Agile Framework (SAFe)](https://www.scaledagileframework.com/)
