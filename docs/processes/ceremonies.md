# Ceremonies

Every structured meeting in SquadFlow is a **Ceremony**. This page catalogs the canonical ones. If your organization needs something beyond this list, see [cadences.md](cadences.md#how-to-add-a-new-cadence) before inventing.

Each entry answers: what is this for, who convenes, who attends, how often, how long, what are the inputs and outputs, and what goes wrong when it is done badly.

## Recurring ceremonies

### Debriefing

**Purpose:** each Player reports, in one sentence or two, what they did today and what they plan tomorrow. Surfaces blockers early.

**Frequency:** daily, end of business.

**Duration:** ≤ 15 minutes. Usually async (message in the Squad's channel).

**Convened by:** Squad Lead (or implicit ritual if live).

**Attendees:** all Players in the Squad.

**Inputs:** each Player's own work.

**Outputs:** a log, date-stamped. Blockers flagged for next Squad Sync.

**Antipatterns:** status theatre ("I worked on some things"); becoming a daily standup with agenda and opinions; skipping it for weeks.

---

### Squad Sync

**Purpose:** weekly alignment inside the Squad. Review the Squad's Tasks, unblock, plan the week ahead.

**Frequency:** weekly.

**Duration:** ~30 minutes.

**Convened by:** Squad Lead.

**Attendees:** all Squad members. Guests allowed for specific items.

**Inputs:** previous week's Debriefings; open Tasks; blockers.

**Outputs:** updated Task assignments; logged blockers with owners; explicit priority for the week.

**Antipatterns:** full-team status report (belongs in Debriefing); debate on Project decisions (belongs in Project meeting); inviting observers until the meeting is 15 people.

---

### Factory Review

**Purpose:** walk the Factory's kanban left to right. Identify stuck cards, reassign if needed, adjust stage definitions, update the operating manual if needed.

**Frequency:** weekly (biweekly for slow-flowing Factories).

**Duration:** ~30 minutes.

**Convened by:** Factory Manager.

**Attendees:** Factory Manager, the Squad members who work the Factory, optional Org Steward for visibility.

**Inputs:** the kanban; throughput metrics from the previous period; open Tasks.

**Outputs:** stuck cards resurfaced; stage definitions refined if needed; proposals for improvement Projects surfaced.

**Antipatterns:** reading the kanban out loud (everyone already has eyes); debating Project-sized changes in the middle of Review (create a Project instead); skipping Reviews when things "feel fine".

---

### Portfolio Review

**Purpose:** Stewards and Leads look at all active Factories and Projects. Are we still investing in the right mix? Is anything drifting? Does a Project need cancellation or absorption soon?

**Frequency:** monthly.

**Duration:** ~60 minutes.

**Convened by:** Org Steward.

**Attendees:** Org Steward(s), Squad Leads, Factory Managers, Project Owners of active Projects.

**Inputs:** Factory throughput, Project health, OKR progress mid-quarter.

**Outputs:** updated portfolio decisions (pause a Factory, cancel a Project, form a new Squad). Decision-log entries for sensitive changes.

**Antipatterns:** becoming a status report (status lives in Debriefings and Squad Syncs); rubber-stamp (Steward agrees with everything); getting into Task-level debate.

---

### OKR Setting and Review

**Purpose:** set OKRs for the next period (at the start) and score the ones from the previous period (at the end). Often run as two sessions within a week.

**Frequency:** quarterly.

**Duration:** ~90 minutes per session.

**Convened by:** OKR Sponsors (drafts) and the Org Steward (approval).

**Attendees:** OKR Sponsors, Org Steward, Squad Leads (for squad-level OKRs), and any Player whose work was central to the OKRs.

**Inputs (Setting):** strategic context from the Strategic Cadence; OKR drafts from Sponsors.

**Outputs (Setting):** OKRs committed (`state = active`), dashboards updated.

**Inputs (Review):** OKR dashboards, Key Result measurements, qualitative context.

**Outputs (Review):** each OKR scored and `closed`. Outcomes (`achieved`, `partially_met`, `missed`) recorded. Learnings captured in decision logs.

**Antipatterns:** using OKR Review as a performance review for Players (different purpose); scoring `committed` OKRs leniently; setting OKRs without baseline data.

---

### Strategic Cadence

**Purpose:** Org Steward reviews direction. What has changed in the market, in the organization, in the opportunity set? What should change in the next quarter's OKRs?

**Frequency:** quarterly, ideally before OKR Setting.

**Duration:** ~120 minutes.

**Convened by:** Org Steward.

**Attendees:** Org Stewards, optionally a small group of senior advisors (CEO + CFO + COO style).

**Inputs:** market signals, revenue trends, OKR scores from the previous period.

**Outputs:** strategic narrative for the next period; feedstock for OKR Setting.

**Antipatterns:** becoming operational (Portfolio Review's job); inviting too many people (erodes candor).

## Ad-hoc ceremonies

These are triggered by lifecycle transitions, not by the calendar.

### Project Kickoff

**Purpose:** mark the transition `backlog → active`. Ensure the Squad, timeline, and deliverables are clear.

**Duration:** ~30–60 minutes.

**Convened by:** Project Owner.

**Attendees:** Project Owner, Squad Lead(s), key Players.

**Output:** Project is `active`; first Tasks are on the board; kickoff notes in the Project's Document.

### Project Closing / Retrospective

**Purpose:** mark the transition to `closed`. Record what happened, what was learned, and the close reason.

**Duration:** ~60 minutes.

**Convened by:** Project Owner.

**Attendees:** Project Owner, Squad members, Org Steward (if cancellation or absorption).

**Output:** `close_reason` recorded; decision-log entry; retrospective notes attached as a Document. For `absorbed`, the new Factory exists and the handoff is complete.

### Squad Formation

**Purpose:** mark `forming → active` for a Squad. Introduce members, agree on mandate and cadence.

**Duration:** ~60 minutes.

**Convened by:** Squad Lead + Org Steward.

**Attendees:** all Squad members.

**Output:** Squad is `active`; first Squad Sync scheduled; mandate documented.

### Squad Dissolution Handoff

**Purpose:** mark `dissolving → dissolved`. Ensure all work is re-homed.

**Duration:** ~60 minutes.

**Convened by:** Org Steward + Squad Lead.

**Attendees:** Squad members, inheriting Squad Leads.

**Output:** every Factory, Project, and open Task has a new home (or is closed). Decision-log entry.

### Factory Retirement Review

**Purpose:** retire a Factory explicitly, not by neglect.

**Duration:** ~45 minutes.

**Convened by:** Org Steward + Factory Manager.

**Attendees:** Squad members running the Factory; optionally successor Squad Leads.

**Output:** `retired` state set. Decision-log entry with rationale. Historical metrics preserved.

## Minimum viable calendar

For a small organization (< 30 people), the minimum useful set is:

- **Daily:** Debriefing (if Squads have ≥ 3 members).
- **Weekly:** Squad Sync per Squad; Factory Review per Factory.
- **Quarterly:** OKR Setting + Review.
- **Ad-hoc:** Kickoff and Closing as Projects demand.

Skip Portfolio Review, Strategic Cadence, and Annual Planning until the org grows into them. Adding ceremonies too early creates theatre and burns goodwill.
