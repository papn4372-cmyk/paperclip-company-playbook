# Paperclip AI Company Playbook

A practical playbook for setting up an AI agent company in Paperclip that actually works.

Every mechanism described here exists because its absence caused real failures in production: rework, wasted tokens, frustrated founders, and broken trust. This is not theory — it is distilled from running multiple companies in parallel and fixing what broke.

*Built by [@aronprins](https://x.com/aronprins) — if you get stuck or need consultancy, DM me. Happy to help :)*

---

## What's included

```
playbook/
├── README.md              ← You are here (the playbook)
└── templates/
    ├── ceo/
    │   ├── SOUL.md        ← CEO identity, beliefs, anti-patterns
    │   ├── HEARTBEAT.md   ← CEO heartbeat state machine (12 steps)
    │   ├── AGENTS.md      ← CEO context, team roster, quality gate
    │   └── TOOLS.md       ← API endpoints, email, file system
    ├── worker-agent/
    │   ├── AGENTS.md      ← Worker identity, DoD, communication protocol
    │   └── HEARTBEAT.md   ← Worker heartbeat with self-check step
    └── company/
        ├── PROJECT-INVENTORY.md  ← Source of truth for what exists
        └── CONTRIBUTING.md       ← Commit conventions, branch strategy
```

Copy the templates, fill in the `[BRACKETS]`, and you have a working company (or have your CEO do it all for you).

---

## How to use this playbook

**Read the playbook first** (this document). It explains *why* each template exists and what it prevents. Then copy the templates and customize them for your company.

The templates are designed to be filled in, not read as-is. Every `[BRACKET]` is a value you need to provide.

---

## The core principle

> **Two layers of verification before anything reaches the Founder.**
>
> Layer 1: The agent checks their own work (self-check in worker HEARTBEAT).
> Layer 2: The CEO checks the agent's work (Quality Control Gate in CEO HEARTBEAT).
>
> If either layer is missing, the Founder becomes the QA department.

This principle drives every template in this playbook.

---

## 1. The files you need

Before your company starts operating, every file below must exist. A missing file is a guaranteed future failure.

| File | Template | What it prevents |
|------|----------|-----------------|
| `PROJECT-INVENTORY.md` | [`templates/company/PROJECT-INVENTORY.md`](templates/company/PROJECT-INVENTORY.md) | Agents recreating existing work |
| `CONTRIBUTING.md` | [`templates/company/CONTRIBUTING.md`](templates/company/CONTRIBUTING.md) | Merge chaos, inconsistent commits |
| `agents/ceo/SOUL.md` | [`templates/ceo/SOUL.md`](templates/ceo/SOUL.md) | CEO acting as postman, identity drift |
| `agents/ceo/HEARTBEAT.md` | [`templates/ceo/HEARTBEAT.md`](templates/ceo/HEARTBEAT.md) | Skipped quality checks, no feedback loops |
| `agents/ceo/AGENTS.md` | [`templates/ceo/AGENTS.md`](templates/ceo/AGENTS.md) | Wrong delegations, lost context |
| `agents/ceo/TOOLS.md` | [`templates/ceo/TOOLS.md`](templates/ceo/TOOLS.md) | Wrong tools, missed API capabilities |
| `agents/[role]/AGENTS.md` | [`templates/worker-agent/AGENTS.md`](templates/worker-agent/AGENTS.md) | Vague ownership, no definition of done |
| `agents/[role]/HEARTBEAT.md` | [`templates/worker-agent/HEARTBEAT.md`](templates/worker-agent/HEARTBEAT.md) | Agents marking broken work as "done" |

---

## 2. The CEO: quality gate, not postman

The CEO is the most critical agent. A good CEO catches problems before the Founder sees them. A bad CEO forwards agent output unchecked and creates a communication layer that slows everything down.

### The CEO SOUL ([`templates/ceo/SOUL.md`](templates/ceo/SOUL.md))

The SOUL defines who the CEO *is*. Without it, the CEO invents their own identity — and that identity is usually "helpful assistant who forwards things quickly." That's the opposite of what you need.

Key sections:
- **"What We Are"** — prevents identity drift. Explicitly state what the company does and what it does NOT do.
- **"Quality Control Is My Most Important Job"** — the single most important belief. Without this, the CEO optimizes for speed instead of correctness.
- **"What I Don't Do"** — explicit anti-patterns. Include "Report work without verifying it" and "Forward agent comments as my own assessment."

### The CEO HEARTBEAT ([`templates/ceo/HEARTBEAT.md`](templates/ceo/HEARTBEAT.md))

The HEARTBEAT is a state machine — 12 steps, always in the same order, no shortcuts. This is where quality control lives.

**The 5 steps that matter most:**

| Step | What it does | What it prevents |
|------|-------------|-----------------|
| **Step 1 — Orient** | Read memory + PROJECT-INVENTORY before doing anything | Duplicate work, stale context |
| **Step 3.5 — Pre-Creation Gate** | 4 questions before creating any task | Busywork, vague tasks, duplicates |
| **Step 4 — Quality Control Gate** | Verify every deliverable via WebFetch before emailing Founder | CEO-as-postman, Founder-as-QA |
| **Step 6 — Anti-Drift Check** | "Am I about to email done without checking?" | Habit regression |
| **Step 9 — Feedback Loop** | After every Founder correction: update instructions, log, verify | Same mistake repeating |

**Step 4 is the highest-impact step.** In production, a CEO had this rule written down but executed zero verification checks over 8 days. The Founder found every bug on the live site — 15+ issues. Making this a numbered, blocking step (not a footnote) eliminates ~60% of rework.

### The "idle is success" principle

Without this principle documented in the SOUL, CEOs treat idle agents as a problem and generate busywork. The SOUL must explicitly state:

> An idle department with finished deliverables is success, not failure. I do not create tasks to keep agents busy. When the Phase backlog is exhausted, I report to the Founder and wait.

---

## 3. Worker agents: self-check before "done"

Every worker agent needs two files: AGENTS.md (who they are) and HEARTBEAT.md (what they do each heartbeat).

### The worker AGENTS.md ([`templates/worker-agent/AGENTS.md`](templates/worker-agent/AGENTS.md))

Key sections that most setups miss:

- **Communication Protocol** — "Paperclip only. No email. No direct Founder contact." Repeat this in every agent file. Agents that can email the Founder will email the Founder.
- **"What I Don't Do"** — Explicit boundaries prevent scope creep.
- **Definition of Done** — Must be concrete and checkable. "Code works" is not a DoD. "Page loads without PHP errors, all links tested, self-check completed" is.

### The worker HEARTBEAT ([`templates/worker-agent/HEARTBEAT.md`](templates/worker-agent/HEARTBEAT.md))

The critical addition: **Step 5 — Self-Check (MANDATORY)**.

Every agent must check their own work before marking it done. The self-check has two parts:

1. **Generic checks** (same for all roles): deliverable exists, matches request, no placeholders
2. **Role-specific checks** (customized per role): the template includes examples for developers, content writers, designers, and engineers

Plus an **anti-patterns table** — starts empty, grows as mistakes happen. This is the institutional memory that prevents the same error from recurring.

---

## 4. PROJECT-INVENTORY.md: the source of truth

([`templates/company/PROJECT-INVENTORY.md`](templates/company/PROJECT-INVENTORY.md))

This file answers the question every agent should ask before starting work: *"Does this already exist?"*

Without it, agents recreate existing deliverables, use wrong product names, or build things that contradict the Founder's vision. The CEO must read this file before every delegation (Step 1 of the HEARTBEAT).

---

## 5. Anti-patterns this playbook prevents

Every mechanism exists because one of these failures happened in production.

| What goes wrong | Why it happens | What prevents it |
|---|---|---|
| **CEO as postman** | CEO forwards agent output without checking | Quality Control Gate (HEARTBEAT Step 4) |
| **Agents don't test their work** | No self-check step in heartbeat | Self-Check (worker HEARTBEAT Step 5) |
| **Same mistake 3 times** | Instructions not updated after corrections | Feedback Loop (HEARTBEAT Step 9) |
| **Agents create busywork** | Idle treated as failure | "Idle is success" in SOUL + Pre-Creation Gate |
| **Identity drift** | Agents forget what the company does | SOUL "What We Are" + Anti-Drift Check |
| **Duplicate work** | Nobody checks what already exists | PROJECT-INVENTORY.md + Pre-Creation Gate |
| **Founder finds all the bugs** | No verification before reporting done | Two-layer verification (agent + CEO) |
| **Lost communication** | Founder unaware of status or blockers | Proactive Communication (Step 8) with dedup |
| **Content format mismatch** | Markdown imported literally into CMS | Format-specific self-check + anti-patterns table |
| **"Explorations" shipped as final** | Designer delivers options, not specs | DoD requires final deliverables, not explorations |
| **Feedback loops don't close** | Instruction updated but fix never verified | Step 9 requires: update + log + verify next time |
| **Stale context between heartbeats** | Agent acts on old information | Memory read (Step 1) + daily notes + PROJECT-INVENTORY |

---

## 6. First-day setup checklist

### Prerequisites

- [ ] Company created in Paperclip (note the Company ID)
- [ ] Git repository initialized
- [ ] Gmail label created for your company prefix (e.g. `abc`)
- [ ] Gmail filter created: subject contains `[PREFIX]` -> apply label

### Setup steps

**1. Create directory structure**
```bash
mkdir -p agents/ceo/memory/daily-notes
mkdir -p company
mkdir -p docs
```

**2. Write `company/vision.md`** — 1-2 paragraphs: what the company does, who the customer is, what success looks like.

**3. Copy and fill in `PROJECT-INVENTORY.md`** from [`templates/company/PROJECT-INVENTORY.md`](templates/company/PROJECT-INVENTORY.md). Define: product, brand, directory ownership, existing assets.

**4. Copy and fill in `CONTRIBUTING.md`** from [`templates/company/CONTRIBUTING.md`](templates/company/CONTRIBUTING.md). Define: agent roles, commit prefixes, branch strategy.

**5. Set up CEO agent** — copy all 4 files from [`templates/ceo/`](templates/ceo/):
- `SOUL.md` — fill in identity, beliefs, north star
- `HEARTBEAT.md` — customize departments, phase backlog, email prefix
- `AGENTS.md` — fill in team roster, company context
- `TOOLS.md` — fill in API details, email addresses, file paths

**6. Set up worker agents** — for each role, `mkdir -p agents/[role-slug]/memory` and copy both files from [`templates/worker-agent/`](templates/worker-agent/):
- `AGENTS.md` — customize identity, responsibilities, DoD
- `HEARTBEAT.md` — customize self-check items, anti-patterns, technical references

**7. Create Phase 1 backlog** in Paperclip: goal -> projects -> issues, all linked.

**8. Start CEO heartbeat** and verify the first cycle:
- [ ] CEO read PROJECT-INVENTORY.md
- [ ] CEO checked Gmail with correct prefix
- [ ] CEO did NOT create tasks outside the Phase backlog
- [ ] CEO noted idle departments as success (not a problem)
- [ ] CEO emailed Founder with initial status

---

## 7. Quality checklist before going live

Before deploying any agent, verify these items. A missing item is a future quality failure.

### CEO agent
- [ ] SOUL.md has "What We Are" and "What We Are NOT"
- [ ] SOUL.md has "Quality Control Is My Most Important Job"
- [ ] SOUL.md has "What I Don't Do" including "report without verifying"
- [ ] HEARTBEAT.md has Quality Control Gate (Step 4) with verification checklist
- [ ] HEARTBEAT.md has Pre-Creation Gate (4 questions)
- [ ] HEARTBEAT.md has Feedback Loop (Step 9)
- [ ] HEARTBEAT.md has Anti-Drift Check (Step 6)
- [ ] HEARTBEAT.md references PROJECT-INVENTORY.md in Step 1
- [ ] HEARTBEAT.md has email dedup rules

### Worker agents
- [ ] AGENTS.md has reporting line (to manager, NOT to Founder)
- [ ] AGENTS.md has concrete Definition of Done (checkable items)
- [ ] AGENTS.md has Communication Protocol (Paperclip only, no email)
- [ ] AGENTS.md has "What I Don't Do"
- [ ] HEARTBEAT.md has self-check step with role-specific checklist
- [ ] HEARTBEAT.md has anti-patterns table (even if empty)
- [ ] HEARTBEAT.md has "if nothing assigned, exit — do not generate work"

### Company files
- [ ] PROJECT-INVENTORY.md exists with product identity and deliverables
- [ ] CONTRIBUTING.md exists with commit conventions
- [ ] company/vision.md exists

---

## 8. Lessons from production

### What works

1. **SOUL.md with explicit boundaries.** "We are X, we are NOT Y" prevents drift. A generic SOUL without guardrails leads to agents building the wrong thing.

2. **Pre-Creation Gate.** 4 questions before any task creation prevents busywork. Without it, CEOs invent tasks to fill idle time.

3. **Phase completion as success.** Without "idle is fine" documented, CEOs treat idle agents as failure and generate waste.

4. **PROJECT-INVENTORY.md as mandatory reading.** Prevents duplicate deliverables. Agents that don't know what exists will recreate it.

5. **Verification evidence in every "done" email.** Requiring the CEO to state what they checked forces actual verification.

### What fails

1. **Rules as footnotes.** A rule like "verify before reporting done" means nothing if it's not a numbered, blocking step. Make it Step 4 in the sequence — not a note at the bottom.

2. **No agent self-check.** Without concrete checklists, agents produce: raw markdown in CMS, missing templates, broken layouts — all caught by the Founder on the live site.

3. **Feedback loops that don't close.** Updating instructions after a correction is not enough. The fix must be verified on the next similar task.

4. **Format mismatches.** Content in markdown imported literally into a system expecting HTML is a classic, predictable failure. The self-check must include format verification.

5. **"Explorations" as deliverables.** 15 design options is not 5 final designs with implementation specs. The DoD must distinguish exploration from completion.

6. **CEO without technical understanding.** If the CEO can't tell a CSS bug from a missing post, they can't be the quality gate. The red flags table (Step 4b) compensates by listing visual symptoms and what they mean.

---

**Need help with your Paperclip setup?** Whether you're stuck or looking for hands-on consultancy, DM me on X ([@aronprins](https://x.com/aronprins)) — happy to help or just point you in the right direction :)
