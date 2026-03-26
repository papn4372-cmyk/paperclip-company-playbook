# Pre-loaded Tasks

## First-Day Setup

Tasks to complete when importing this company package.

### 1. Configure Company Identity

- **Assignee:** CEO
- **Priority:** High
- **Description:** Fill in all `[BRACKET]` placeholders across company files: SOUL.md, HEARTBEAT.md, AGENTS.md, TOOLS.md. Define company name, mission, product, tech stack, team roster, email prefix, and primary business goal.
- **Acceptance Criteria:**
  - [ ] No `[BRACKET]` placeholders remain in any agent file
  - [ ] Company name, mission, and product are defined in SOUL.md
  - [ ] Team roster is filled in AGENTS.md and HEARTBEAT.md
  - [ ] Email prefix and Gmail configuration set in HEARTBEAT.md
  - [ ] Primary business goal (North Star) defined in SOUL.md

### 2. Create PROJECT-INVENTORY.md

- **Assignee:** CEO
- **Priority:** High
- **Description:** Create the source-of-truth document listing all existing work, product details, design references, directory ownership, and infrastructure. This file must exist before any agent starts working.
- **Acceptance Criteria:**
  - [ ] Product identity defined (name, domain, what we are / are not)
  - [ ] Directory ownership table filled in
  - [ ] Current phase documented
  - [ ] Rules for all agents section completed

### 3. Set Up Worker Agents

- **Assignee:** CEO
- **Priority:** Medium
- **Description:** For each department role needed, create agent directories and customize AGENTS.md and HEARTBEAT.md from the worker template. Customize the self-check with role-specific items.
- **Acceptance Criteria:**
  - [ ] Each worker agent has `agents/{role-slug}/AGENTS.md` with identity, DoD, and communication protocol
  - [ ] Each worker agent has `agents/{role-slug}/HEARTBEAT.md` with role-specific self-check items
  - [ ] Each worker agent has a `memory/` directory
  - [ ] All agents listed in CEO's team roster

### 4. Create Phase 1 Backlog

- **Assignee:** CEO
- **Priority:** Medium
- **Description:** Create the initial goal, projects, and issues in Paperclip. All issues must be linked to a goal and project. Do not create tasks outside the approved phase backlog.
- **Acceptance Criteria:**
  - [ ] At least one goal created in Paperclip
  - [ ] Projects linked to goal
  - [ ] Issues created with clear acceptance criteria
  - [ ] Every issue has `goalId`, `projectId`, and `status: todo`

### 5. Verify First CEO Heartbeat

- **Assignee:** CEO
- **Priority:** Medium
- **Description:** Run the first complete CEO heartbeat cycle and verify all 12 steps execute correctly.
- **Acceptance Criteria:**
  - [ ] CEO read PROJECT-INVENTORY.md
  - [ ] CEO checked Gmail with correct prefix
  - [ ] CEO did NOT create tasks outside the Phase backlog
  - [ ] CEO noted idle departments as success (not a problem)
  - [ ] CEO emailed Founder with initial status including verification evidence
