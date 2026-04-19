# Ontology

The catalog of the nine first-class entities. Each file documents what the entity *is*; lifecycles are in [`../lifecycles/`](../lifecycles/); the formal schemas in [`../data-model/schemas/`](../data-model/schemas/).

For the layered overview and relationships, see the main [README](../../README.md).

## The nine entities

| Layer | Entity | File |
|---|---|---|
| Context | Company | [`company.md`](company.md) |
| Context | Brand | [`brand.md`](brand.md) |
| Strategy | OKR | [`okr.md`](okr.md) |
| Execution | Factory | [`factory.md`](factory.md) |
| Execution | Project | [`project.md`](project.md) |
| Execution | Squad | [`squad.md`](squad.md) |
| Execution | Task | [`task.md`](task.md) |
| People | Player | [`player.md`](player.md) |
| Knowledge | Document | [`document.md`](document.md) |

## File template

```markdown
# <Entity>

> One-sentence definition.

One paragraph of purpose — what problem this entity solves, how it differs from the adjacent one.

## Attributes

| Name | Type | Required | Description |
| ... table ... |

Authoritative list: [`../data-model/schemas/<entity>.schema.json`](../data-model/schemas/).

## Relations

- bullets describing cardinality and role names.

## Lifecycle

`state_a → state_b → ...`. See [`../lifecycles/<entity>.md`](../lifecycles/).

## Example

One short narrative.

## Antipatterns

- **Name** — one-sentence trap and fix.
```

## Style

- Second person, short sentences.
- Concrete over abstract; every file has one example and ≥ 2 antipatterns.
- Cross-link the glossary ([`../concepts/glossary.md`](../concepts/glossary.md)) on first mention of a term.
- No marketing tone — that belongs in the [README](../../README.md).
