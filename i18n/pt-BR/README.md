<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="../../docs/assets/logo-dark.png">
    <img src="../../docs/assets/logo.png" alt="SquadFlow" width="128">
  </picture>
</p>

<h1 align="center">SquadFlow</h1>

<p align="center">
  <strong>Fábricas tocam seu negócio. Projetos mudam seu negócio.</strong>
</p>

<p align="center">
  Um framework aberto para administração de empresas que equilibra <em>execução contínua</em> e <em>iniciativas temporárias</em>.<br>
  Uma ontologia, nove entidades, três camadas — e um modelo de dados formal pensado para um futuro sistema proprietário.
</p>

<p align="center">
  <a href="../../LICENSE"><img src="https://img.shields.io/badge/license-CC--BY--SA%204.0-blue.svg" alt="Licença: CC-BY-SA 4.0"></a>
  <img src="https://img.shields.io/badge/version-v1.0%20em%20andamento-orange.svg" alt="Versão">
  <img src="https://img.shields.io/badge/idioma_fonte-Inglês-informational.svg" alt="Idioma fonte: Inglês">
  <a href="https://github.com/guilhermej/squadflow-framework/stargazers"><img src="https://img.shields.io/github/stars/guilhermej/squadflow-framework?style=social" alt="GitHub stars"></a>
</p>

<p align="center">
  <img src="../../docs/assets/hero-v2.png" alt="Modelo de três camadas do SquadFlow — Contexto, Estratégia, Execução, Pessoas e Conhecimento" width="960">
</p>

> [!NOTE]
> Esta é a versão em português do SquadFlow. A **fonte da verdade é o [README em inglês](../../README.md)** — diferenças devem ser tratadas como erro de tradução e corrigidas via PR. Terminologia canônica PT-BR na tabela abaixo.

> [!IMPORTANT]
> **Em uma frase:**
> Trabalho contínuo e trabalho de mudança são disciplinas diferentes, e a maioria dos frameworks finge que não são.
> SquadFlow mantém os dois separados — e nomeia o momento em que uma mudança bem-sucedida vira rotina.

## O SquadFlow é para você?

| ✅ Sim, se você é… | ❌ Não, se você é… |
|---|---|
| Um founder, COO ou chief of staff em uma empresa de **10 a 200 pessoas**. | Um time de 5 pessoas. Basta conversar. |
| Opera **mais de uma marca, linha de produto ou unidade de negócio**. | Um único time Scrum em um único produto — fica com Scrum. |
| Cansado de emendar Scrum + Kanban + OKRs + "processo" com durex. | Já está 500+ pessoas dentro de SAFe — trocar custa caro. |
| Disposto a pagar o pequeno imposto de **nomear as coisas explicitamente**. | Alérgico a ontologia. |
| Planejando eventualmente construir software *em cima* do seu modelo operacional. | Procurando uma trilha de certificação. Aqui não tem. |

## Terminologia canônica PT-BR

| 🇺🇸 Inglês | 🇧🇷 Português (termo canônico) |
|---|---|
| Company | Empresa |
| Brand | Marca |
| OKR | OKR (mantido) |
| Factory | Fábrica |
| Project | Projeto |
| Squad | Squad (mantido) |
| Task | Tarefa |
| Player | Player (mantido) |
| Document | Documento |
| Squad Lead, Factory Manager, Project Owner, OKR Sponsor, Org Steward | Mantidos em inglês (terminologia comum no mercado tech brasileiro) |
| States (`active`, `paused`, `closed`, …) | Mantidos em inglês — batem com o JSON Schema |

## Conteúdo

1. [Por que SquadFlow](#por-que-squadflow)
2. [Os cinco princípios](#os-cinco-princípios)
3. [As nove entidades](#as-nove-entidades)
4. [Ciclos de vida em resumo](#ciclos-de-vida-em-resumo)
5. [Pilha de cadências](#pilha-de-cadências)
6. [Roles](#roles)
7. [Governança](#governança)
8. [Quickstart](#quickstart)
9. [Como o SquadFlow se compara](#como-o-squadflow-se-compara)
10. [Modelo de dados](#modelo-de-dados)
11. [Quem usa](#quem-usa)
12. [Pronto pra testar?](#pronto-pra-testar)
13. [Referência completa](#referência-completa)
14. [Contribuindo & licença](#contribuindo--licença)

## Por que SquadFlow

Tocar uma empresa são duas tarefas diferentes.

**Uma é manter o negócio vivo** — fechar vendas toda semana, produzir conteúdo, atender suporte, processar folha de pagamento. O trabalho não para. O objetivo é ritmo.

**A outra é mudar o negócio** — lançar um produto, migrar um sistema, entrar em um novo mercado. O trabalho tem começo, meio e fim. O objetivo é entrega.

Pegue um funil de vendas. `Prospect → Qualificado → Proposta → Ganho`. Ele nunca esvazia. Na semana que vem vão chegar novos prospects, quer você tenha planejado quer não. Isso é uma **Fábrica**. Forçar isso em sprints de duas semanas é erro de categoria.

Agora pegue *"migrar nosso sistema de cobrança de um código próprio para o Stripe"*. Tem escopo, tem início, tem fim. Quando terminar, terminou — o Stripe toca sozinho. Isso é um **Projeto**. Seria absurdo colocar isso no kanban do time de vendas.

A maioria dos frameworks escolhe um dos lados e finge que o outro é caso especial. Scrum otimiza mudança em sprints. Kanban otimiza fluxo e chama tudo de ticket. SAFe tenta fazer os dois e desaba sob o próprio peso. SquadFlow separa os dois desde o primeiro dia — nos lifecycles, nos schemas de dados, nas regras de governança.

> [!TIP]
> **O que a maioria dos frameworks perde:** quando um Projeto é bem-sucedido e produz algo que *precisa* ser operado pra sempre (um portal de parceiros, um novo pipeline de contratação, um canal de conteúdo), SquadFlow tem um estado dedicado pra essa transição — `absorbed`. O Projeto fecha; nasce uma nova Fábrica. Nenhum trabalho fica invisível. Nenhuma ownership evapora.

Se essa formulação clica para você, continue lendo. Se não clica, nenhum framework vai resolver — o problema está em outro lugar.

## Os cinco princípios

1. **Fábricas tocam seu negócio. Projetos mudam seu negócio.** Uma Fábrica é permanente; um Projeto tem começo, escopo e fim.
2. **Toda entidade tem um único dono.** Nunca um comitê. Se ninguém é pessoalmente responsável, a coisa drifta — é lei da física, não opinião.
3. **Estados são explícitos.** "Feito" não é um estado. "Em progresso" não é um estado. Um estado é um dos itens de uma lista finita e curta, com condições documentadas de entrada e saída. Ambiguidade sobre status é a principal causa de trabalho parado, e trabalho parado é silencioso.
4. **Estratégia e execução compartilham um modelo.** OKRs são cidadãos de primeira classe no mesmo grafo que Fábricas, Projetos e Squads — não uma ferramenta separada mantida por um time separado.
5. **Aberto por padrão.** [CC-BY-SA 4.0](../../LICENSE). Adapte, traduza, construa em cima. Cite a origem. Mantenha derivados abertos.

Motivação completa: [MANIFESTO.md](../../MANIFESTO.md) (em inglês).

## As nove entidades

A ontologia do SquadFlow tem **nove entidades de primeira classe em quatro camadas**. Nem mais, nem menos.

### 🌍 Contexto — onde o trabalho acontece

- 🏢 **Empresa (Company)** — Uma pessoa jurídica (LLC/Ltda/Corp) que assina contratos e paga impostos. Exemplo: *Guardsi Tecnologia LTDA*.
- 🆔 **Marca (Brand)** — Uma identidade comercial pertencente a uma Empresa. Exemplo: *Solyd*, *Caveiratech* — ambas carregadas pela mesma Empresa.

### 🎯 Estratégia — por que o trabalho acontece

- 🎯 **OKR** — Objetivo e Resultados-Chave para um período, pontuado no fechamento. Exemplo: *"Ser a plataforma preferida de billing para SaaS LATAM"* com 2–4 KRs mensuráveis.

### ⚙️ Execução — como o trabalho acontece

- 🏭 **Fábrica (Factory)** — Produção contínua. Exemplo: *Fábrica de Vendas B2B* com etapas `Prospect → Qualificado → Proposta Enviada → Em Negociação → Ganho`.
- 🚀 **Projeto (Project)** — Iniciativa temporária. Exemplo: *Migração de Billing para Stripe* — começa em fevereiro, termina em maio, fecha com `delivered`.
- ⚔️ **Squad** — Time multifuncional. Exemplo: *Squad de Plataforma* de 6 (3 engenheiros, 1 designer, 1 PM, 1 Lead) rodando uma Fábrica + um Projeto.
- ✅ **Tarefa (Task)** — Unidade atômica de trabalho. Exemplo: *"Escrever o módulo connector do Stripe"*, atribuída à Ana, bloqueada aguardando acesso a produção, prazo 10 de maio.

### 🏀 Pessoas & Conhecimento — quem executa e o que persiste

- 🏀 **Player** — O indivíduo. Exemplo: Ana entra como `candidate`, vira `active` no primeiro dia, é promovida a Squad Lead seis meses depois.
- 📄 **Documento (Document)** — Conhecimento registrado. Exemplo: *Manual Operacional da Fábrica de Vendas*, de responsabilidade do Factory Manager, marcado `outdated` se não for revisado por 6 meses.

### Relações principais

- Uma **Empresa** possui muitas **Marcas**, emprega **Players**, roda **Fábricas** e escopa **OKRs** e **Projetos**.
- Uma **Marca** pode escopar seus próprios **OKRs**, **Projetos** e **Fábricas**.
- Um **Squad** é responsável por rodar **Fábricas** e executar **Projetos**. Também pode ter **OKRs** em nível de squad.
- Toda **Tarefa** pertence a exatamente uma **Fábrica**, **Projeto** ou **Squad**, e é atribuída a exatamente um **Player**.
- **OKRs** são contribuídos por **Fábricas**, **Projetos** e **Squads** (muitos-para-muitos).
- Um **Projeto** bem-sucedido que produz saída contínua é *absorbed* numa nova **Fábrica** no fechamento.
- **Documentos** se anexam a qualquer entidade para persistência de conhecimento.

Schema completo com cardinalidades: [`docs/data-model/er-diagram.svg`](../../docs/data-model/er-diagram.svg).

## Ciclos de vida em resumo

Toda entidade tem uma máquina de estados finita. Diagramas completos em [`docs/lifecycles/`](../../docs/lifecycles/); resumo abaixo.

| Entidade | Estados | Transição-chave |
|---|---|---|
| Empresa | `active → archived` | Arquivada apenas em dissolução legal. |
| Marca | `active → archived` | Arquivada quando descontinuada no mercado. |
| OKR | `draft → active → in_review → closed` | No fechamento: `achieved` (score ≥ 0.7), `partially_met` ou `missed`. |
| Fábrica | `proposed → active ⇄ paused → retired` | Aposentadoria exige aprovação de Steward + Manager. |
| Projeto | `idea → scoping → backlog → active → delivery → closed` | Razão de fechamento: `delivered`, `canceled`, ou **`absorbed`** em uma nova Fábrica. |
| Squad | `forming → active ⇄ on_hold → dissolving → dissolved` | Dissolução repassa todas as Fábricas/Projetos explicitamente. |
| Tarefa | `todo → in_progress ⇄ blocked → done` | Razão de conclusão: `completed` ou `canceled`. |
| Player | `candidate → active ⇄ on_leave → offboarded` | Offboarding reatribui Tarefas e retira da composição do Squad; registro preservado. |
| Documento | `draft → in_review → published ⇄ outdated → archived` | `outdated` é flag de primeira classe — docs desatualizados são marcados, não escondidos. |

> [!NOTE]
> A transição `absorbed` é o movimento mais importante do SquadFlow. Quando um Projeto bem-sucedido precisa ser operado continuamente, vira uma nova Fábrica — com um novo Manager, um novo kanban e um registro no decision log explicando por quê.

## Pilha de cadências

| Frequência | Cerimônia | Escopo | Duração | Convocada por |
|---|---|---|---|---|
| Diária | Debriefing | todos os Players | ≤ 15 min | Squad Lead |
| Semanal | Squad Sync | por Squad | ~30 min | Squad Lead |
| Semanal | Factory Review | por Fábrica | ~30 min | Factory Manager |
| Mensal | Portfolio Review | Stewards + Leads | ~60 min | Org Steward |
| Trimestral | OKR Setting / Review | organização inteira | ~90 min por sessão | OKR Sponsors |
| Trimestral | Strategic Cadence | Stewards | ~120 min | Org Steward |
| Anual | Planejamento Anual + OKRs | organização inteira | um dia inteiro | Org Steward |

Mais as cerimônias ad-hoc disparadas por transições de lifecycle (Project Kickoff, Project Closing, Squad Formation, Squad Dissolution, Factory Retirement).

> [!TIP]
> Não rode tudo isso no primeiro dia. Uma empresa de 20 pessoas sobrevive com Debriefing diário + Squad Sync semanal + OKR Review trimestral. Adicione mais quando sentir a falta — não porque o framework pede.

Detalhes: [`docs/processes/cadences.md`](../../docs/processes/cadences.md) · [`docs/processes/ceremonies.md`](../../docs/processes/ceremonies.md).

## Roles

Roles são responsabilidades nomeadas assumidas por Players. Um Player pode assumir várias Roles ao mesmo tempo. Roles não são cargos, não são níveis de remuneração.

| Role | Escopo | Responsabilidade |
|---|---|---|
| **Player** | individual | Executa Tarefas; participa das cerimônias do Squad. |
| **Squad Lead** | 1 Squad | Coordena o Squad; garante que a cadência rode. |
| **Factory Manager** | 1 Fábrica | Dono do kanban; roda o Review semanal; mantém manual operacional. |
| **Project Owner** | 1 Projeto | Responsável pela entrega; decide razão de fechamento. |
| **OKR Sponsor** | N OKRs | Modela, defende e pontua o OKR. |
| **Org Steward** | 1 Empresa ou Marca | Aprova transições de estado; *não* microgerencia. |

Detalhes: [`docs/processes/roles.md`](../../docs/processes/roles.md).

## Governança

**Quatro princípios:**

1. Toda entidade tem um único dono — nunca um comitê.
2. Aprovações são logadas — transições sensíveis criam entrada no decision log.
3. Stewards não microgerenciam — aprovam transições de estado, não Tarefas.
4. Roles não são cargos — responsabilidades nomeadas, não níveis de remuneração.

**Quem aprova o quê (resumo):**

| Ação | Aprovador(es) |
|---|---|
| Criar / arquivar Empresa, Marca | Org Steward |
| Criar Fábrica | Org Steward |
| Aposentar Fábrica | Org Steward + Factory Manager |
| Criar Projeto | Project Owner (+ OKR Sponsor se ligado a OKR) |
| Cancelar Projeto | Project Owner + Org Steward |
| Absorver Projeto → Fábrica | Project Owner + Org Steward |
| Formar / dissolver Squad | Squad Lead + Org Steward |
| Definir / fechar OKR | OKR Sponsor |
| Offboard Player | RH + Org Steward |
| Publicar Documento | Dono (após review) |
| Atribuir / cancelar Tarefa | Squad Lead, Factory Manager ou Project Owner |

RACI completa e padrão de decision log: [`docs/processes/governance.md`](../../docs/processes/governance.md).

## Quickstart

<p>
  <img src="https://img.shields.io/badge/⏱_15_min-lightgray" alt="15 minutos"> <img src="https://img.shields.io/badge/🧩_sem_instalação-lightgray" alt="Sem instalação"> <img src="https://img.shields.io/badge/📝_funciona_em_Notion,_papel,_qualquer_coisa-lightgray" alt="Funciona em Notion, papel, qualquer coisa">
</p>

1. **Crie uma Empresa e uma Marca.** Mesmo uma startup de marca única cria as duas — elas vão divergir no dia que você crescer.
2. **Identifique suas Fábricas e seus Projetos.** Um funil de vendas é uma Fábrica. Construir uma funcionalidade nova é um Projeto. Se nunca acaba, é Fábrica. Se tem prazo, é Projeto.
3. **Escolha 1 a 3 OKRs para o trimestre.** Objetivo + 2 a 4 Resultados-Chave mensuráveis. Atribua um Sponsor a cada um. Menos de 1 significa que você está no piloto automático; mais de 3 significa que nada é prioridade.
4. **Forme seus Squads.** Multifuncional, 2+ Players, um Squad Lead. Atribua Fábricas e Projetos.
5. **Defina sua cadência.** Debriefing diário, Squad Sync semanal, Factory Review semanal, OKR Setting/Review trimestral.

> [!TIP]
> Bateu numa dúvida que a doc não respondeu óbvio? Três lugares para olhar:
>
> - **O que é essa coisa?** → [`docs/ontology/`](../../docs/ontology/)
> - **Em que estado ela pode estar?** → [`docs/lifecycles/`](../../docs/lifecycles/)
> - **Quem aprova?** → [`docs/processes/governance.md`](../../docs/processes/governance.md)

Passo a passo detalhado: [`docs/getting-started.md`](../../docs/getting-started.md). Template Notion baixável: lançamento com a v1.0 em [`templates/notion/`](../../templates/notion/).

## Como o SquadFlow se compara

| Dimensão | **SquadFlow** | Scrum | Shape Up | SAFe | Só OKRs |
|---|---|---|---|---|---|
| Escopo | empresa inteira | um time | time de produto | enterprise | só estratégia |
| Operações contínuas | **Fábrica (primeira classe)** | não nativo | não modelado | periférico | invisível |
| Iniciativas temporárias | **Projeto (primeira classe)** | sprints | bets | epics | — |
| Ligação com estratégia | **OKR nativo, relacional** | externa | qualitativa | epics↔OKRs | é a própria coisa |
| Multi-marca | **sim** | não | não | em escala enterprise | não |
| Modelo de dados | **JSON Schemas** | informal | informal | informal | informal |
| Licença | **CC-BY-SA 4.0** | Attribution-ShareAlike | CC-BY-NC-ND | proprietária | domínio público |
| Tamanho alvo | 10–200 | 5–15 | 5–30 | 500+ | qualquer |

Comparações detalhadas por framework: [`docs/comparisons/`](../../docs/comparisons/).

**Quando escolher outra coisa, honestamente:**

- **Time de 5** → sem framework. Frameworks são pra quando a comunicação começa a quebrar. Você não está lá ainda.
- **Um único time Scrum, um produto** → Scrum. Sério, pare de adicionar coisa.
- **Enterprise, 500+ engenheiros, já comprometida com SAFe** → fique. Trocar não é de graça. SquadFlow não escala pro seu formato de qualquer jeito.
- **Procurando certificações e uma rede de coaches** → SAFe ou Scrum.org. SquadFlow não oferece nenhum dos dois e não planeja.

## Modelo de dados

SquadFlow vem com um **modelo de dados formal**: nove JSON Schemas (draft 2020-12), um diagrama ER e convenções de nomenclatura. Validado em CI; gera clientes idiomáticos sem ajuste manual.

```bash
# TypeScript
npx json-schema-to-typescript docs/data-model/schemas/project.schema.json

# Python (Pydantic)
datamodel-codegen --input docs/data-model/schemas/project.schema.json \
  --output project.py --input-file-type jsonschema
```

Fonte: [`docs/data-model/`](../../docs/data-model/) — convenções, ER, 9 schemas, fixtures de teste.

> [!NOTE]
> A maioria dos frameworks de gestão é entregue apenas em prosa. SquadFlow é entregue como prosa *e* um contrato legível por máquina. Isso é intencional — esperamos que alguém construa software proprietário em cima, e preferimos que parta de schemas válidos em vez de opiniões parafraseadas.

## Quem usa

<p align="center">
<strong>1 Grupo</strong> · <strong>2 Empresas</strong> · <strong>5 Marcas</strong> · <strong>usado diariamente desde 2024</strong>
</p>

**[Grupo Solyd](https://solyd.com.br)** — o framework nasceu aqui, foi estressado aqui e é a razão pela qual cada decisão na v1.0 é opinativa do jeito que é.

- **Guardsi** — serviços B2B de cibersegurança e educação.
- **Mindz** — plataformas SaaS para negócios de infoproduto.
- **Solyd** — educação em cibersegurança (maior da América Latina).
- **Caveiratech** — conteúdo e mídia.
- **Solyd Hunter** — programa de talentos.

Estudo de caso detalhado: [`examples/multi-brand-group.md`](../../examples/multi-brand-group.md) (com a v1.0).

> [!NOTE]
> Rodando SquadFlow na sua organização? Abra uma Issue ou PR para se adicionar aqui. Credibilidade é composta.

## Pronto pra testar?

<table>
<tr>
<td align="center" width="33%">
  <a href="https://github.com/guilhermej/squadflow-framework">⭐</a><br>
  <strong><a href="https://github.com/guilhermej/squadflow-framework">Star no repo</a></strong><br>
  <sub>Acompanhe a evolução até a v1.0</sub>
</td>
<td align="center" width="33%">
  <a href="../../templates/notion/">📥</a><br>
  <strong><a href="../../templates/notion/">Baixar template Notion</a></strong><br>
  <sub>Importa, popula, tá rodando (v1.0)</sub>
</td>
<td align="center" width="33%">
  <a href="../../MANIFESTO.md">📖</a><br>
  <strong><a href="../../MANIFESTO.md">Ler o Manifesto</a></strong><br>
  <sub>O framework inteiro em 400 palavras (EN)</sub>
</td>
</tr>
</table>

## Referência completa

Para leitura aprofundada — especialmente se você vai implementar o framework como software ou adotá-lo formalmente:

| Área | O que está lá |
|---|---|
| [Manifesto](../../MANIFESTO.md) | Os cinco princípios, em forma estendida. |
| [Glossário](../../docs/concepts/glossary.md) | Definições canônicas de cada termo. |
| [Ontologia](../../docs/ontology/) | Um arquivo por entidade — atributos, relações, exemplos, antipadrões. |
| [Lifecycles](../../docs/lifecycles/) | Máquinas de estado por entidade — diagramas, transições, comportamento. |
| [Processos](../../docs/processes/) | Roles, cadências, cerimônias, governança — em profundidade. |
| [Modelo de dados](../../docs/data-model/) | JSON Schemas, ER, orientação para geração de clientes. |
| [Comparações](../../docs/comparisons/) | SquadFlow vs. Scrum / Shape Up / SAFe / OKRs (detalhado). |
| [Getting started](../../docs/getting-started.md) | Passo a passo de 15 minutos. |
| [Template Notion](../../templates/notion/) | Workspace starter importável (com a v1.0). |
| [Exemplos](../../examples/) | Casos trabalhados — SaaS fictícia, Grupo Solyd. |

## Contribuindo & licença

Contribuições, traduções e adaptações são bem-vindas.

| Canal | Para |
|---|---|
| [**Issues**](https://github.com/guilhermej/squadflow-framework/issues) | Bugs, erros de digitação, ambiguidade, sugestões de funcionalidade. |
| [**Discussions**](https://github.com/guilhermej/squadflow-framework/discussions) | Perguntas abertas, debates de design, showcases. |
| [**Pull requests**](https://github.com/guilhermej/squadflow-framework/pulls) | Correções, refinamentos, traduções. Ver [CONTRIBUTING.md](../../CONTRIBUTING.md). |
| [**Security advisories**](https://github.com/guilhermej/squadflow-framework/security/advisories) | Disclosures sensíveis — ver [SECURITY.md](../../SECURITY.md). |

Antes de contribuir, leia [CONTRIBUTING.md](../../CONTRIBUTING.md) e [CODE_OF_CONDUCT.md](../../CODE_OF_CONDUCT.md).

**Licença:** [CC-BY-SA 4.0](../../LICENSE). Você pode compartilhar, adaptar e construir produtos comerciais em cima — desde que cite a origem e mantenha derivados sob a mesma licença. Atribuições devem apontar para <https://github.com/guilhermej/squadflow-framework>.

## Agradecimentos

SquadFlow se apoia nos ombros de frameworks que vieram antes:

- **Andy Grove** e **John Doerr** pela disciplina de OKRs.
- **Basecamp / Ryan Singer** por Shape Up e a disciplina de shaping/betting emprestada no estado `scoping` de Projetos.
- **Spotify** pelo termo *Squad* (usado aqui com significado mais estreito — e sim, sabemos que a própria Spotify não usa mais o "Spotify Model").
- **Scrum.org** pelo Scrum Guide, cuja disciplina editorial inspirou o tom desta documentação.

O framework nasceu dentro do [**Grupo Solyd**](https://solyd.com.br) e é testado diariamente contra a realidade. Se quebra lá, é consertado aqui.

---

<table align="center">
<tr>
<td>
  <strong>Guilherme Junqueira Soares</strong><br>
  CEO — <a href="https://solyd.com.br">Solyd Research</a><br>
  guilherme[at]solyd[.]com[.]br · <a href="https://github.com/guilhermej">@guilhermej</a>
</td>
<td align="center" width="260">
  <a href="https://github.com/guilhermej/squadflow-framework/stargazers"><img src="https://img.shields.io/github/stars/guilhermej/squadflow-framework?style=social" alt="Stars"></a>
  <a href="https://github.com/guilhermej/squadflow-framework/watchers"><img src="https://img.shields.io/github/watchers/guilhermej/squadflow-framework?style=social" alt="Watchers"></a>
  <a href="https://github.com/guilhermej/squadflow-framework/forks"><img src="https://img.shields.io/github/forks/guilhermej/squadflow-framework?style=social" alt="Forks"></a>
</td>
</tr>
</table>

<p align="center">
  <sub>
    <strong>SquadFlow é um framework jovem.</strong> A v1.0 é o primeiro release público; a ontologia pode evoluir com feedback.<br>
    Feito com cuidado no Brasil · <a href="../../CHANGELOG.md">Changelog</a> · © 2026 Guilherme Junqueira Soares · <a href="../../LICENSE">CC-BY-SA 4.0</a>
  </sub>
</p>
