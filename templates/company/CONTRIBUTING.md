# Contributing — [COMPANY NAME]

Commit conventions and contribution guidelines for all agents.

---

## Commit Conventions

All agents must use the following format:

```
[agent-role]: short description ([PREFIX]-XX)
```

### Agent Roles

| Role | Commit prefix |
|------|--------------|
| CEO | `[ceo]` |
| [ROLE 1] | `[role-slug]` |
| [ROLE 2] | `[role-slug]` |

### Examples

```
[ceo]: update HEARTBEAT with quality gate ([PREFIX]-10)
[founding-engineer]: fix API endpoint validation ([PREFIX]-15)
[wp-developer]: implement homepage layout ([PREFIX]-3)
```

---

## Rules for All Agents

1. **Always commit after completing an issue.** Do not leave work uncommitted.
2. **Reference the issue identifier** (e.g. `[PREFIX]-64`) at the end of the commit message.
3. **One commit per issue** is the norm. Multiple commits only if work spans multiple sessions.
4. **Never commit secrets.** `.env` files, API keys, and passwords must never be committed.

---

## After Each Completed Issue

1. Stage and commit changes:
   ```bash
   git add <specific files>
   git commit -m "[your-role]: description ([PREFIX]-XX)"
   ```
2. Update the issue status in Paperclip to `done`.
3. Post a comment on the issue with what was done and relevant links.
4. If your work affects another agent's task, post a comment on their issue.

---

## Branch Strategy

[CHOOSE ONE:]

Option A — All on main (early MVP phase):
> All agents work on `main` directly during MVP phase. No feature branches required until post-launch.

Option B — Feature branches (mature company):
> All agents work on feature branches. PRs are required. Only the Founder merges development PRs into `main`. CEO may merge content-only PRs when verified correct.

---

## File Ownership

| Directory | Owner |
|-----------|-------|
| `[DIR 1]` | [ROLE] |
| `[DIR 2]` | [ROLE] |
| `docs/` | All agents (read), relevant owner (write) |
| `agents/` | CEO (write), relevant agent (read) |
