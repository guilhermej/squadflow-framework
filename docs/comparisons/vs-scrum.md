# SquadFlow vs. Scrum

## TL;DR

Scrum describes how a single team iterates on a single product backlog in 2-week sprints. SquadFlow describes the layer *above* — where many squads, factories, projects, and OKRs coexist in the same organization. They are complementary, not competitive: a SquadFlow Squad can still run Scrum internally.

## What Scrum does well

- **Team-level iteration.** Scrum's sprint / planning / review / retrospective rhythm is a well-tested way to run an engineering team on a continuous backlog of product work.
- **Mental simplicity.** Three roles, three artifacts, five events. You can teach it in an afternoon.
- **30 years of adoption.** Certifications, books, coaches, case studies. If you hire a Scrum Master, they will know what they are doing.
- **Self-organizing teams.** Scrum is deliberately vague about how decisions get made inside the team, which works well when the team is small and cohesive.

## Where Scrum is limited

- **Team-level scope only.** Scrum has nothing to say about multiple teams, multiple brands, operational work that is not product development, OKR alignment, or organizational governance.
- **No first-class support for continuous operations.** Sales, content, support, and billing do not fit naturally into "sprints" with "user stories". Scrum teams running these workflows end up forcing ceremonies that do not match the work.
- **No link to strategy.** Scrum does not describe how a sprint goal connects to a quarterly OKR or a company-level direction. That is left as an exercise to the reader.
- **Product backlog as a single queue.** Scrum treats everything as items on one list. SquadFlow distinguishes Factories (continuous) from Projects (temporary) because they have different shapes.

## What SquadFlow adds

- **Factories** for continuous operations — explicitly permanent, weekly-reviewed, separately governed.
- **OKR as a first-class entity** with formal relations to Factories, Projects, and Squads.
- **Multi-brand, multi-squad governance** — Org Stewards, Brand Stewards, a decision-log pattern.
- **A formal data model** (JSON Schemas, ER) so the framework can scale beyond prose.
- **Project lifecycle that includes `absorbed`** — a successful Project that becomes a continuous Factory, a motion Scrum does not name.

## Side-by-side

| Dimension | Scrum | SquadFlow |
|---|---|---|
| Scope | Single team | Whole organization |
| Time frame | 2-week sprints | Daily → yearly cadence stack |
| Continuous ops | Not native | Factories (first-class) |
| Temporary initiatives | Native (Sprint goals, backlog) | Projects (first-class) |
| Strategy link | External | OKR native and relational |
| Data model | Informal | JSON Schemas per entity |
| License | Attribution ShareAlike (Scrum Guide) | CC-BY-SA 4.0 |
| Adoption breadth | Massive | Nascent |

## When to pick Scrum instead

- Your entire company is one product engineering team and the work is essentially iterative product development. You do not need governance beyond the team. Scrum will cost you less overhead than SquadFlow.
- You already have Scrum muscle — certifications, coaches, conventions — and the pain you are solving is inside a team, not across the organization.

## Using Scrum inside SquadFlow

SquadFlow does not tell you how to run work *inside* a Squad. A Squad can absolutely adopt Scrum for its own cadence:

- The Squad's **Scrum Sprint Planning** produces Tasks on the Squad's Factories and active Projects.
- The Squad's **Daily Standup** and **Sprint Review** are the same events SquadFlow calls **Debriefing** and **Squad Sync** — you can overlap them.
- The Squad's **Retrospective** becomes part of the SquadFlow Project Closing ceremony when a Project ends.

If this is how you want to operate, say so in the Squad's description. It changes nothing in the SquadFlow governance.

## Migrating from pure Scrum to SquadFlow

Practical steps if your organization runs Scrum today and wants to adopt SquadFlow as the layer above:

1. **Catalog your work by shape.** For each kind of work your company does, decide: Factory (continuous) or Project (temporary)? Create the records.
2. **Map your Scrum Teams to Squads.** A Scrum Team is typically one Squad. Name the Squad Lead (the Scrum Master, usually — or the Tech Lead).
3. **Assign existing Factories and Projects to Squads.** Be explicit. If two Squads share ownership of a Factory, pick one and note the other as a contributor.
4. **Introduce OKRs.** Set 1–3 company-level OKRs and map each Squad's work to at least one.
5. **Keep your sprints.** Sprints are a Squad-internal concern. Nothing in SquadFlow asks you to stop.
6. **Add the Factory Review weekly.** If a Squad owns a Factory, walk its kanban once a week. This is where continuous work becomes visible.
7. **Start a decision log.** Any sensitive transition (starting a Project, retiring a Factory, dissolving a Squad) gets a short dated entry with the rationale.

## See also

- [Manifesto](../../MANIFESTO.md)
- [Ontology](../ontology/)
- [Governance](../processes/governance.md)
