# SquadFlow vs. Shape Up

## TL;DR

Shape Up is a rigorous, opinionated method for running product teams in 6-week cycles with a 2-week cooldown. Its mental models (shaping, betting, appetite, the hill chart) are first-rate. But Shape Up only describes product-building work — it has no answer for continuous operations, multi-brand governance, or OKR alignment. SquadFlow covers the whole organization; for the specific case of a Squad running a change-oriented Project, Shape Up's shaping and betting practices are directly borrowable.

## What Shape Up does well

- **Shaping.** Before a Project starts, Shape Up insists on a shaping phase where the problem, solution sketch, and rabbit holes are explored by senior people. This is one of the best ideas in modern software management.
- **Betting with appetite.** A bet is a fixed time box (6 weeks by default) plus a rough appetite ("big batch" or "small batch"). The team delivers something within the time or the bet dies. Scope flexes to time.
- **Hill chart over percent-done.** Instead of "we are 60% done", Shape Up teams report where on the hill they are (still discovering vs. executing). Matches reality better than percentage-based progress.
- **Cooldown.** Two weeks between 6-week cycles. Teams pay tech debt, explore, and recover. The absence of cooldown is why most iterative frameworks burn teams out.
- **Self-contained book.** [Shape Up](https://basecamp.com/shapeup) by Ryan Singer is free online and readable in a weekend.

## Where Shape Up is limited

- **Product teams only.** Shape Up describes change-oriented product development. It has nothing to say about a sales pipeline, a content calendar, a customer-success operation, or a recruiting pipeline.
- **Scope is one team at a time.** If you have three Squads, Shape Up does not tell you how they coordinate, how they share a product vision, or how they map to OKRs.
- **No OKRs, no strategy layer.** Bets are decided by "shapers" (usually co-founders) based on feel. There is no formal link between a bet and a company-level objective.
- **No governance layer.** Decisions about what to bet on are described prescriptively ("shapers decide") but without a general model for who approves what across the organization.
- **Restrictive license.** Shape Up is CC-BY-NC-ND — you can read it, you cannot adapt it, you cannot build commercial derivatives. This is deliberate, but it limits how the community evolves the method.

## What SquadFlow adds

- **Factories and Projects as separate entities.** Shape Up's bets map roughly to SquadFlow Projects. Continuous work (which Shape Up does not model) becomes Factories.
- **OKR as first-class.** Bets in Shape Up are justified qualitatively. SquadFlow Projects formally link to OKRs.
- **Multi-squad organization.** Shape Up describes one team; SquadFlow describes many.
- **Formal data model.** Shape Up is prose; SquadFlow is prose + JSON Schemas.
- **Open license.** CC-BY-SA 4.0. You can adapt, translate, and build on it.

## Side-by-side

| Dimension | Shape Up | SquadFlow |
|---|---|---|
| Scope | Single product team | Whole organization |
| Time frame | 6-week cycle + 2-week cooldown | Daily → yearly cadence stack |
| Continuous ops | Not modeled | Factories (first-class) |
| Temporary initiatives | Bets (the core unit) | Projects (first-class) |
| Shaping phase | Rigorously defined | Informal (part of `scoping`) |
| Strategy link | Shapers' judgement | OKR native and relational |
| Data model | Informal | JSON Schemas per entity |
| License | CC-BY-NC-ND | CC-BY-SA 4.0 |
| Proof of use | Basecamp + many public adopters | Grupo Solyd + open adoption |

## When to pick Shape Up instead

- You are a small product-focused company (~5–30 people, one main product), and you want a prescriptive, end-to-end method for running product development.
- You want the full shape-it → bet-it → build-it → cool-down cycle out of the box, without the freedom to adapt it.
- You do not yet have enough organizational complexity (multiple brands, multiple squads, operational work) for SquadFlow to be worth its overhead.

## Using Shape Up inside SquadFlow

A Squad running a Project can absolutely use Shape Up for that Project:

- The Project's `scoping` state is where shaping happens. The shaped pitch lives as a Document attached to the Project.
- The Project's `active` state becomes a 6-week cycle. At the end, if not `delivered`, the Project either extends explicitly (with a decision-log entry explaining why) or is canceled — in the spirit of Shape Up's "circuit breaker".
- The Squad's cooldown weeks map naturally to a Squad with no active Projects — the Squad runs Factories only, ships no change-work, rests.

SquadFlow does not prescribe this. It is one pattern among many.

## Migrating from Shape Up to SquadFlow

If your organization has grown past Shape Up's comfort zone:

1. **Name your Factories.** Shape Up never modeled them; you have been running them unofficially (support queue, sales motion, recruiting). Make them first-class.
2. **Keep your betting table as the Project pipeline.** The Shape Up betting table becomes the `backlog` queue of SquadFlow Projects.
3. **Introduce OKRs.** Bets that were chosen by feel now link to explicit objectives.
4. **Formalize governance.** Shape Up leaves decisions to "shapers" implicitly. SquadFlow names Org Stewards, OKR Sponsors, and Project Owners.
5. **Keep shaping.** It is a strength. Build it into the `scoping` state of Projects as a standard.

## See also

- [Manifesto](../../MANIFESTO.md)
- [Project ontology](../ontology/project.md)
- [Shape Up](https://basecamp.com/shapeup) by Ryan Singer (Basecamp)
