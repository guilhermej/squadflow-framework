# Glossary

Canonical definitions of every term used in SquadFlow. When a term in another file seems imprecise, this glossary is the source of truth.

Terms are alphabetical. Entities in **bold** have dedicated files under [`../ontology/`](../ontology/).

---

### Absorbed

A terminal state of a **Project**, meaning the project succeeded and produced an outcome that now needs to be operated continuously. The project is closed; a new **Factory** is created to continue the work.

### Attribute

A named property of an entity (e.g., `name`, `owner_id`, `state`). The canonical list of attributes per entity lives in [`../data-model/schemas/`](../data-model/schemas/).

### **Brand**

A commercial identity owned by one or more companies. A company can have multiple brands; one brand usually belongs to one company. See [`../ontology/brand.md`](../ontology/brand.md).

### Cadence

The rhythm at which a ceremony repeats (daily, weekly, monthly, quarterly, yearly). The full cadence stack lives in [`../processes/cadences.md`](../processes/cadences.md).

### Ceremony

A structured, recurring meeting with a defined purpose, attendees, inputs and outputs. Examples: Debriefing, Squad Sync, Factory Review, Portfolio Review. See [`../processes/ceremonies.md`](../processes/ceremonies.md).

### Closed

A terminal state of a **Project** (with a close reason: delivered, canceled, or absorbed) or of an **OKR** (with a score).

### **Company**

A legal entity (CNPJ, Ltd, LLC). Companies employ Players, own Brands, run Factories and sponsor Projects and OKRs. See [`../ontology/company.md`](../ontology/company.md).

### Decision log

A dated record of a sensitive decision attached to the entity it affects. Triggered automatically by some state transitions (e.g., `absorb project → factory`, `retire factory`). See [`../processes/governance.md`](../processes/governance.md).

### **Document**

Recorded knowledge attached to one or more entities. Manuals, policies, meeting notes, design docs, standard operating procedures. See [`../ontology/document.md`](../ontology/document.md).

### Entity

A first-class concept in the SquadFlow ontology. v1.0 has nine: Company, Brand, OKR, Factory, Project, Squad, Task, Player, Document.

### **Factory**

A unit of continuous production. Same output, repeatedly. Permanent by nature; retires only when the business no longer needs that output. See [`../ontology/factory.md`](../ontology/factory.md).

### Factory Manager

The Role responsible for the operational health of one Factory. Approves factory-scoped decisions, runs the weekly Factory Review, surfaces risks. See [`../processes/roles.md`](../processes/roles.md).

### Governance

The rules for who approves what. Documented as a RACI matrix. See [`../processes/governance.md`](../processes/governance.md).

### Kanban

A visual board where each column is a stage of a process and each card is a work item. Factories always have a kanban. Projects may have one during the active state. SquadFlow does not reinvent kanban — it adopts it.

### Layer

One of three groupings of entities in the ontology: **Context** (Company, Brand), **Strategy** (OKR), **Execution** (Factory, Project, Squad, Task), **People & Knowledge** (Player, Document).

### Lifecycle

The set of states an entity can be in, plus the allowed transitions between them. Every entity has a lifecycle file under [`../lifecycles/`](../lifecycles/).

### **OKR**

Objective + Key Results. A commitment at company, brand, or squad level to achieve a measurable outcome over a period (usually a quarter). See [`../ontology/okr.md`](../ontology/okr.md).

### OKR Sponsor

The Role responsible for defining an OKR, defending it, and closing it with a score. Typically a steward or a squad lead.

### Ontology

The formal catalog of entities, their attributes and their relations. SquadFlow's ontology is the center of gravity of the framework.

### Org Steward

The Role responsible for the overall health of a Company or a Brand. Approves high-level transitions (create/retire factory, cancel project, dissolve squad).

### **Player**

An individual who executes work. A Player belongs to one or more Squads and is assigned to Tasks. See [`../ontology/player.md`](../ontology/player.md).

### **Project**

A temporary initiative with a start, a scope and an end. Produces a defined outcome and then closes. See [`../ontology/project.md`](../ontology/project.md).

### Project Owner

The Role accountable for delivering a specific Project. Owns the scope, the cadence and the close decision.

### RACI

A governance shorthand: **R**esponsible (does the work), **A**ccountable (owns the outcome), **C**onsulted (gives input), **I**nformed (is notified). SquadFlow emphasizes the single accountable owner and is less strict about R/C/I.

### Relation

A named link between two entities (e.g., `Squad → responsible_for → Factory`). Relations are part of the ontology and are formalized in the data model.

### Role

A named responsibility that a Player can take on. Canonical roles: Player, Squad Lead, Factory Manager, Project Owner, OKR Sponsor, Org Steward. A person can hold several roles simultaneously. See [`../processes/roles.md`](../processes/roles.md).

### Schema

The JSON Schema definition for an entity, under [`../data-model/schemas/`](../data-model/schemas/). Used for validation and for code generation in a future proprietary system.

### **Squad**

A cross-functional team of two or more Players, working on one or more Factories or Projects. See [`../ontology/squad.md`](../ontology/squad.md).

### Squad Lead

The Role responsible for coordinating a Squad, ensuring the squad's cadence runs, and surfacing impediments.

### State

One of the finite named statuses an entity can be in (e.g., a Project can be `idea`, `scoping`, `backlog`, `active`, `delivery`, or `closed`). Every entity's states are listed in its Lifecycle file.

### **Task**

An atomic unit of work assigned to a single Player. Belongs to a Factory, Project, or Squad. See [`../ontology/task.md`](../ontology/task.md).

### Transition

A named arrow between two states in a lifecycle (e.g., `scoping → active`). Every transition names the role that triggers it and any side effects that follow.
