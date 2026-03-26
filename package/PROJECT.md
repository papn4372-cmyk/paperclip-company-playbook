# Project Definitions

## Company Setup

The primary project when importing this package. Establishes the agent company structure with all verification mechanisms in place.

### Workspace Bindings

| Path | Purpose |
|------|---------|
| `agents/ceo/` | CEO agent home — SOUL, HEARTBEAT, TOOLS, AGENTS |
| `agents/ceo/memory/daily-notes/` | CEO daily notes and institutional memory |
| `agents/{role-slug}/` | Worker agent home — AGENTS, HEARTBEAT |
| `agents/{role-slug}/memory/` | Worker agent memory |
| `company/` | Company-level documents (vision, inventory) |
| `docs/` | Shared documentation |

### Required Files

These files must exist before the company starts operating:

| File | Purpose |
|------|---------|
| `PROJECT-INVENTORY.md` | Source of truth for existing work — prevents duplicate deliverables |
| `CONTRIBUTING.md` | Commit conventions and branch strategy for all agents |
| `agents/ceo/SOUL.md` | CEO identity, beliefs, anti-patterns — prevents identity drift |
| `agents/ceo/HEARTBEAT.md` | CEO 12-step state machine — ensures quality checks run |
| `agents/ceo/AGENTS.md` | CEO context, team roster, quality gate responsibility |
| `agents/ceo/TOOLS.md` | API endpoints, email configuration, file system paths |
| `agents/{role}/AGENTS.md` | Worker identity, responsibilities, Definition of Done |
| `agents/{role}/HEARTBEAT.md` | Worker heartbeat with mandatory self-check |

### Core Principle

> Two layers of verification before anything reaches the Founder.
>
> Layer 1: The agent checks their own work (self-check in worker HEARTBEAT).
> Layer 2: The CEO checks the agent's work (Quality Control Gate in CEO HEARTBEAT).
>
> If either layer is missing, the Founder becomes the QA department.
