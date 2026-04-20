# SquadFlow Framework — Claude Code instructions

You are assisting with the **SquadFlow Framework** — an open company management framework (CC-BY-SA 4.0). This file gives Claude Code the project-specific context, conventions, and guardrails it needs to help well.

## Project identity

- **What:** An open management framework (9 entities, 3 layers). Public repo, MIT-compatible license.
- **Source of truth:** This repo (`github.com/guilhermej/squadflow-framework`). English (`docs/**`, `README.md`) is canonical; PT-BR (`i18n/pt-BR/**`) is a derived translation.
- **Audience:** Founders, COOs, and chiefs of staff at 10–200 person scale-ups and multi-brand groups.
- **License:** [CC-BY-SA 4.0](LICENSE). Derivatives must stay open; attributions must link back to this repo.

The framework's five principles are in [`MANIFESTO.md`](MANIFESTO.md). Read that before editing conceptual content — the framework is opinionated and the principles should show through.

## Canonical files

| File | Purpose |
|---|---|
| [`README.md`](README.md) | One-page full reference. If you change the ontology, lifecycles, processes, or any first-class concept — this file must stay in sync. |
| [`MANIFESTO.md`](MANIFESTO.md) | The five principles. Short by design. Don't bloat it. |
| [`docs/ontology/`](docs/ontology/) | One file per first-class entity. Pattern is strict — see [`docs/ontology/README.md`](docs/ontology/README.md) for the template. |
| [`docs/lifecycles/`](docs/lifecycles/) | State machine per entity. Every enum state must match the corresponding JSON Schema in `docs/data-model/schemas/`. |
| [`docs/processes/`](docs/processes/) | Roles, cadences, ceremonies, governance. |
| [`docs/data-model/schemas/`](docs/data-model/schemas/) | Nine JSON Schemas (draft 2020-12). Validated in CI. |
| [`docs/comparisons/`](docs/comparisons/) | SquadFlow vs. Scrum / Shape Up / SAFe / OKRs. |
| [`i18n/pt-BR/README.md`](i18n/pt-BR/README.md) | PT-BR translation of the main README. Must stay paired. |

## Editing conventions

- **EN first.** All conceptual changes land in English first. PT translation follows in a later PR.
- **Terminology is canonical.** The 9 entities have fixed names (Company / Brand / OKR / Factory / Project / Squad / Task / Player / Document). PT-BR equivalents in the [terminology table](i18n/pt-BR/README.md#terminologia-canônica-pt-br). Do not invent new ones.
- **States are enums, not prose.** Every lifecycle file's states must match its JSON Schema exactly. If they disagree, the JSON Schema wins — fix the lifecycle file.
- **Tone:** second person, short sentences, concrete examples, ≥ 2 antipatterns per entity. Refer to [`docs/ontology/README.md`](docs/ontology/README.md#style) for the style guide.
- **Line endings:** LF (`\n`). `.gitattributes` enforces this — don't override.
- **Commit messages:** Conventional Commits — `feat:`, `docs:`, `chore:`, `ci:`, `i18n:`, `assets:`, `fix:`, `data-model:`. Scope is optional: `docs(ontology): clarify factory retirement`.

## Anti-leak policy

The file [`examples/multi-brand-group.md`](examples/) describes Grupo Solyd publicly. It is intentionally open, but has guardrails. **Never include in any PR**:

- Real client names
- Revenue, margins, or financial numbers
- Proprietary scripts, prompts, automation code
- Internal tool screenshots with sensitive UI
- Internal Slack/Notion URLs
- Specific deal stages, win rates, pipeline conversion rates
- Individual compensation
- Named prospects

Any PR touching `examples/multi-brand-group.md` requires review by the repository owner before merge. When you generate examples, default to fictional (*Helios*, *Ana*) unless explicitly told to use Solyd context.

## Local testing

### Validate JSON Schemas + fixtures

```bash
# One-time setup
python -m venv .venv
source .venv/bin/activate
pip install 'jsonschema>=4.20'

# Run
python <<'PY'
import json, pathlib
from jsonschema import Draft202012Validator, ValidationError
for p in sorted(pathlib.Path('docs/data-model/schemas').glob('*.schema.json')):
    e = p.stem.replace('.schema', '')
    s = json.load(open(p))
    Draft202012Validator.check_schema(s)
    v = Draft202012Validator(s)
    v.validate(json.load(open(f'docs/data-model/schemas/_test_fixtures/{e}.valid.json')))
    try:
        v.validate(json.load(open(f'docs/data-model/schemas/_test_fixtures/{e}.invalid.json')))
        print(f'FAIL: {e} invalid was accepted')
    except ValidationError:
        print(f'OK: {e}')
PY
```

### Re-render the ER diagram

```bash
npm i -D @mermaid-js/mermaid-cli  # if not installed globally
npx mmdc -i docs/data-model/er-diagram.mermaid \
  -o docs/data-model/er-diagram.svg -t neutral -b transparent
```

### Markdown lint (CI also runs this)

```bash
npx markdownlint-cli2 "**/*.md"
```

## CI checks (see `.github/workflows/lint.yml`)

- `markdownlint-cli2` on all `*.md`.
- JSON Schema validation (meta-schema + valid/invalid fixtures).

Before pushing, run the local commands above. CI failures are usually MD034 (bare URL), MD045 (image alt text missing), MD001 (heading skip), MD040 (fenced code without language).

## Security

Report vulnerabilities via [Security Advisories](https://github.com/guilhermej/squadflow-framework/security/advisories). See [`SECURITY.md`](SECURITY.md) for scope.

Never commit:
- Real secrets, API keys, tokens, or environment files.
- Personal data about contributors beyond their public GitHub profile.
- Files from any private sibling project on the same machine (respect `CLAUDE.local.md` if present — it is gitignored and holds private context).

## Project owner

Guilherme Junqueira Soares — CEO, Solyd Research.
Contact via [Security Advisories](https://github.com/guilhermej/squadflow-framework/security/advisories) for sensitive matters, or via Issues/PRs for everything else.
