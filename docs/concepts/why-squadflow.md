# Why SquadFlow

SquadFlow exists because **running a company is two different jobs**, and most frameworks pretend it is one.

## The core tension

One job is **keeping the business alive** — closing deals every week, shipping content, answering support, processing payroll, invoicing, onboarding new customers. The work never stops. The goal is rhythm.

The other job is **changing the business** — launching a new product, migrating a system, entering a new market, rebuilding a sales motion, rewriting an onboarding. The work has a beginning and an end. The goal is delivery.

They are different disciplines. Continuous work is optimized by consistency and small improvements; change work is optimized by scope discipline and on-time delivery. The same person often does both in the same week, but the work itself is not the same shape.

Most management frameworks pick one side and pretend the other is a special case:

- **Scrum** optimizes change into sprints. It describes a team inside one ongoing product backlog, where everything is worked in 2-week increments. It is excellent inside an engineering squad. It does not describe a sales pipeline, a content calendar, or a partner-onboarding process — nor does it describe how a company's OKRs link to what a team is shipping.
- **Kanban Method** optimizes flow and calls every piece of work a ticket. It is excellent for operations. It is silent on which work is a project, which work is continuous, who owns what, how decisions are escalated, and how teams stay aligned to strategy.
- **SAFe** tries to describe both. It is a heavyweight enterprise framework with many roles, artifacts, and events. It works in very large organizations willing to commit to certification and ceremony, and it scales poorly downward — 100-person companies using SAFe spend as much energy on the framework as on the work.
- **Shape Up** (Basecamp) has real contrarian ideas — shaping before betting, cycles, appetite — but is scoped to product teams doing change work. It does not describe a factory at all.
- **OKRs alone** is a goal-setting discipline, not a framework. OKRs tell you what you are trying to achieve but say nothing about how your teams, kanbans, and cadences organize themselves to get there.

Each of these does something well. None of them describe **the whole job of administering a company**.

## Why SquadFlow names both

SquadFlow names **Factories** and **Projects** as first-class, different, permanent entities in the organization's model.

A **Factory** is a permanent kanban. It produces the same kind of outcome repeatedly — sales calls closed, articles published, bugs fixed, candidates hired. It is run by a Squad, led by a Factory Manager, and reviewed weekly. It does not get "completed"; it gets retired when the business no longer needs the output.

A **Project** is a temporary initiative. It has a start, a scope, and an end. It is run by a Squad, led by a Project Owner, and closed with one of three outcomes: delivered (and finished), canceled, or — the interesting case — **absorbed**. A successful Project that produced something that must now be operated forever is absorbed into a new Factory. This transition is the most important motion in SquadFlow. It is the moment a change becomes a routine.

The split between Factory and Project is not rhetorical. It is formal:

- They have different lifecycles (see [`../lifecycles/`](../lifecycles/)).
- They have different governance (see [`../processes/governance.md`](../processes/governance.md)).
- They have different cadences (see [`../processes/cadences.md`](../processes/cadences.md)).
- They have different schemas (see [`../data-model/schemas/`](../data-model/schemas/)).

## Why OKRs are native, not bolted on

Most frameworks treat OKRs as a parallel track — a Notion page off to the side of the real work. SquadFlow keeps **OKR** as a first-class entity in the same graph as Factories, Projects, and Squads. The contribution is a relation in the data model (`contributed_by`), not a sentence in a slide.

This means any factory, project, or squad can truthfully answer *"which objective am I serving?"* If the answer is *"none"*, the organization has a legible problem it can address. OKRs stop being compliance theatre and become navigation.

## Why a formal data model matters

SquadFlow ships with **nine JSON Schemas** (one per entity), an ER diagram, and naming conventions that survive language and tool changes. A framework without a formal model is a collection of opinions; a framework with one is a specification.

The payoff is threefold:

1. **Consistency.** When the ontology and the schemas agree, teaching the framework becomes teaching one system, not several overlapping mental models.
2. **Portability.** The framework runs on Notion today, could run on Airtable or a custom tool tomorrow, and eventually on a proprietary SquadFlow system. The data model is the contract that lets that migration happen.
3. **Leverage.** Generated clients (TypeScript, Pydantic, Go) drop in without manual massage, because the schemas are strict and self-consistent.

See [`../data-model/`](../data-model/) for the full spec.

## Who this is for

SquadFlow is written for **founders, COOs, and chiefs of staff at scale-ups and multi-brand groups**. Specifically:

- Companies with **10–200 people**.
- Companies operating **more than one brand, product line, or business unit**, or expecting to within 12 months.
- Organizations where ad-hoc coordination has already started to break and a 200-page certification framework would be overkill.
- Leaders who believe ontology and formalism matter, and are willing to pay the small tax of naming things explicitly.

## Who this is NOT for

- **Teams of five.** You do not need a framework. You need to talk to each other.
- **Pure engineering shops running one product with one Scrum team.** Scrum is fine. Do not add SquadFlow just because it exists.
- **Enterprises already deep in SAFe or similar.** SquadFlow is not a drop-in replacement; switching has real switching cost. Stay where you are unless the pain is acute.
- **People looking for a certification track.** SquadFlow is open and self-taught. No exams, no coach network, no badges.

## The punchline

If you remember one sentence from this document, remember this:

> **Factories run your business. Projects change it.**

Every other claim in SquadFlow hangs off that distinction. If it clicks for you, read the [Manifesto](../../MANIFESTO.md), then the [Overview](./overview.md), then the [Ontology](../ontology/). If it does not click, no framework will help; the problem is somewhere else.

## What to read next

- [Manifesto](../../MANIFESTO.md) — the five principles in one page.
- [Overview](./overview.md) — the three-layer model.
- [Getting started](../getting-started.md) — use SquadFlow in 15 minutes.
- [Comparisons](../comparisons/) — SquadFlow vs. Scrum, Shape Up, SAFe, OKRs alone.
