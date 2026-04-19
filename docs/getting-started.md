# Getting started

Use SquadFlow in your organization in **15 minutes**. No software to install. No certifications to pursue.

This guide assumes you have skimmed the [Overview](./concepts/overview.md). If you have not, read that first (3 minutes).

## What you need

- A shared workspace. Notion, Airtable, Google Docs, even a whiteboard — whatever your team already uses. A downloadable Notion template ships with v1.0.
- One hour on the calendar with your co-founders or leadership team for the first setup.
- Honesty about the shape of your work. SquadFlow names things explicitly; half-truths will surface fast.

## Step 1 — Company and Brand (3 minutes)

Create two records.

- **Company** — your legal entity. Name, legal name, tax ID, jurisdiction. If you have one LLC/Ltda/Corp, you create one Company. If you have a group with two separate legal entities, create two.
- **Brand** — your market-facing identity. Name, website, tagline. A single company can carry multiple Brands.

A small startup with one product creates one Company and one Brand with the same name. That is fine. Keeping them separate costs nothing and pays off the day you add a second product line.

See [`docs/ontology/company.md`](docs/ontology/company.md) and [`docs/ontology/brand.md`](docs/ontology/brand.md).

## Step 2 — Factories and Projects (5 minutes)

Walk through the work your organization does and split it into two buckets.

**Factories (continuous, repeated output):**

- Sales pipeline
- Content production
- Customer support
- Recruiting pipeline
- Customer onboarding
- Billing and invoicing
- Monthly close and financial reporting

**Projects (bounded, start-and-end):**

- Launch feature X
- Migrate from vendor A to vendor B
- Enter a new market
- Redesign the onboarding flow
- Build a partner program

For each Factory, define:

- Its name (*"B2B Sales"*, *"Content Calendar"*, *"Customer Onboarding"*).
- The kanban stages (at least 2). For sales: `Prospect → Qualified → Proposal → Won`.
- Who runs it (**Factory Manager**).
- Which Squad is responsible.

For each Project, define:

- Its name and one-line scope.
- The **Project Owner** (one person, accountable for delivery).
- Which Squad(s) will execute.
- An estimated start and end.

See [`docs/ontology/factory.md`](docs/ontology/factory.md) and [`docs/ontology/project.md`](docs/ontology/project.md).

## Step 3 — OKRs (3 minutes)

Pick **1 to 3 OKRs for the quarter**. More than three and nothing is a priority.

Each OKR has:

- **Objective** — a clear direction (*"Become the preferred billing platform for LATAM SaaS startups"*).
- **2–4 Key Results** — measurable outcomes with baseline and target (*"ARR: from $180k to $320k"*).
- A **Sponsor** — the person accountable for the OKR.
- A **commitment type** — `committed` (you will score honestly and be accountable) or `aspirational` (stretch, missing is acceptable).

For each Factory and Project you defined in Step 2, link the OKRs they contribute to. If a piece of work cannot point to any OKR, ask whether it should be happening.

See [`docs/ontology/okr.md`](docs/ontology/okr.md).

## Step 4 — Squads (2 minutes)

A **Squad** is a cross-functional team of 2+ Players.

For most small companies, the first Squads form naturally:

- **Product / Engineering Squad** — builds and maintains the product.
- **Go-to-Market Squad** — sales and marketing.
- **Operations Squad** — finance, HR, legal.

Each Squad has:

- A **name** and a one-line mandate.
- A **Squad Lead** — one Player, coordinates the Squad.
- **Members** — all Players on the Squad, including the Lead.
- One or more Factories or Projects it is responsible for.

See [`docs/ontology/squad.md`](docs/ontology/squad.md).

## Step 5 — Cadence (2 minutes)

Schedule four recurring meetings:

| When | What | Duration |
|---|---|---|
| Every day (end of day) | **Debriefing** — async, each Player writes what they did and what is blocking them. | 10 min |
| Once a week, per Squad | **Squad Sync** — review work, unblock, plan the week. | 30 min |
| Once a week, per Factory | **Factory Review** — walk the kanban left to right. | 30 min |
| Once a quarter | **OKR Setting + Review** — set next quarter's OKRs, score the last one's. | 90 min per session |

Skip anything you do not need yet. A startup with one Squad running one Factory does not need a monthly Portfolio Review. Add ceremonies when you feel the gap, not before.

See [`docs/processes/cadences.md`](docs/processes/cadences.md).

## That's it

You are running SquadFlow.

Within the first week you will hit a question that is not obviously answered — usually about what state a thing is in, who approves a decision, or how to split a fuzzy chunk of work. The documentation is organized to answer those questions without asking you to read it all up front:

- **What is this thing?** → [`docs/ontology/`](docs/ontology/)
- **What state can it be in?** → [`docs/lifecycles/`](docs/lifecycles/)
- **Who approves it?** → [`docs/processes/governance.md`](docs/processes/governance.md)
- **When do we discuss it?** → [`docs/processes/ceremonies.md`](docs/processes/ceremonies.md)

## Growing into more

As the organization grows past ~30 people, you will want to add:

- **Portfolio Review** — monthly, Stewards + Leads look at the full portfolio of Factories and Projects.
- **Strategic Cadence** — quarterly, Stewards look at direction.
- **Annual Planning** — yearly, full-day OKR setting for the year.

See [`docs/processes/cadences.md`](docs/processes/cadences.md) for the full stack.

## When things feel off

The framework is working when people can answer three questions without hesitation:

1. *"What Factory or Project is this Task for?"*
2. *"What OKR does this Factory or Project contribute to?"*
3. *"Who owns this?"*

When any of those are fuzzy, the framework is drifting. Fix the fuzziness, not the framework.
