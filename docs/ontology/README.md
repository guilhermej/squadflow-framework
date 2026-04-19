# Ontology

The SquadFlow ontology is the **formal catalog of nine first-class entities**, their attributes, and their relations. This folder is the single source of truth for what each entity *is*.

For *how an entity evolves over time*, see [`../lifecycles/`](../lifecycles/). For *how it is formally defined for software*, see [`../data-model/`](../data-model/).

## The nine entities

| Layer | Entity | Purpose | File |
|---|---|---|---|
| **Context** | [Company](company.md) | Legal entity (CNPJ/LLC/Ltd). Employs Players, owns Brands, runs Factories, sponsors OKRs. | [`company.md`](company.md) |
| | [Brand](brand.md) | Commercial identity belonging to one Company. Scopes Projects and some OKRs. | [`brand.md`](brand.md) |
| **Strategy** | [OKR](okr.md) | Objective + Key Results for a period. Set by a Company, Brand or Squad; contributed to by Factories, Projects and Squads. | [`okr.md`](okr.md) |
| **Execution** | [Factory](factory.md) | Continuous production unit. Permanent. Owns a kanban. Run by a Squad. | [`factory.md`](factory.md) |
| | [Project](project.md) | Temporary initiative with defined start, scope and end. Can become a Factory when absorbed. | [`project.md`](project.md) |
| | [Squad](squad.md) | Cross-functional team of two or more Players. Responsible for Factories and Projects. | [`squad.md`](squad.md) |
| | [Task](task.md) | Atomic unit of work assigned to a single Player. Lives on a Factory, Project or Squad. | [`task.md`](task.md) |
| **People & Knowledge** | [Player](player.md) | The individual. Belongs to Squads. Holds Roles. | [`player.md`](player.md) |
| | [Document](document.md) | Recorded knowledge attached to one or more other entities. | [`document.md`](document.md) |

See [`../concepts/overview.md`](../concepts/overview.md) for a visual map of how these connect.

## File template

Every entity file in this folder follows the same structure. If you are adding a new entity (candidate for v1.1+) or editing an existing one, start from this template.

```markdown
# <Entity Name>

> One-sentence definition.

## Purpose

Two or three paragraphs answering:
- What is this entity for?
- What problem does it solve?
- How does it differ from the entity it is most easily confused with?

## Attributes

| Name | Type | Required | Description | Example |
|------|------|----------|-------------|---------|
| `id` | UUID v4 | yes | Canonical identifier. | `550e8400-...` |
| `name` | string | yes | Human-readable name. | `Sales factory` |
| `state` | enum | yes | See lifecycle. | `active` |
| ... | ... | ... | ... | ... |

The authoritative attribute list is the corresponding JSON Schema at
[`../data-model/schemas/<entity>.schema.json`](../data-model/schemas/). If the
table and the schema disagree, the schema wins — fix the file.

## Relations

- `<this>` is owned by `<parent>` (cardinality, role).
- `<this>` → `<other>` (cardinality, role).
- `<other>` → `<this>` (cardinality, role).

## Lifecycle

Brief summary of the state machine (1–2 sentences) and a link:

> See [`../lifecycles/<entity>.md`](../lifecycles/) for the full state diagram,
> states, transitions and state-dependent behavior.

## Examples

At least **two concrete examples**. One short, one longer. Real-world examples from
Grupo Solyd are welcome — within the project's [anti-leak policy](../../CONTRIBUTING.md#anti-leak-policy).

### Example 1 — <title>

Short narrative, 2–4 sentences.

### Example 2 — <title>

Longer narrative, 1–2 paragraphs. Walk through at least one state transition.

## Antipatterns

At least **two common misuses**. Each one:

- A short name in bold
- One or two sentences describing the trap and why it matters

**Example antipattern title.** Description of why this is a bad idea and what to do instead.

## See also

- Glossary: [`../concepts/glossary.md`](../concepts/glossary.md)
- Overview: [`../concepts/overview.md`](../concepts/overview.md)
- Lifecycle: [`../lifecycles/<entity>.md`](../lifecycles/)
- Schema: [`../data-model/schemas/<entity>.schema.json`](../data-model/schemas/)
- Related entities: ...
```

## Style rules for entity files

- **Second person.** Address the reader as *you*.
- **Short sentences.** Aim for 15–20 words on average.
- **Concrete over abstract.** Every entity must include at least two real examples and at least two antipatterns.
- **Cross-link liberally.** When a term appears for the first time, link it to its glossary entry.
- **No marketing tone.** Keep the voice neutral and technical. Marketing voice belongs in [`../../README.md`](../../README.md) and [`../concepts/why-squadflow.md`](../concepts/why-squadflow.md).
- **One entity per file.** Never mix entities in a single file. If two entities feel inseparable, that is a signal that the ontology has a bug — open an Issue.
