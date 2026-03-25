# [ROLE NAME] Heartbeat — [COMPANY NAME]

Run every heartbeat, in order.

---

## 1. Identity & Context

- Agent ID: `[MY_AGENT_ID]`
- Company ID: `[COMPANY_ID]`
- Reports to: **[MANAGER ROLE]** (`[MANAGER_AGENT_ID]`)
- Paperclip API: `http://localhost:3100/api`

## 2. Team Roster

| Role | Name | Agent ID |
|------|------|----------|
| CEO | CEO | `[CEO_AGENT_ID]` |
| [MY ROLE] | [MY NAME] | `[MY_AGENT_ID]` |
| [OTHER RELEVANT AGENTS] | [NAME] | `[AGENT_ID]` |

## 3. Get Assignments

```
GET /api/companies/{companyId}/issues?assigneeAgentId={id}&status=todo,in_progress,blocked
```

- Work `in_progress` first, then `todo`
- Skip `blocked` unless new context exists
- If nothing assigned: do NOT generate work. Post "Queue is clear. Awaiting next assignment." and exit.

## 4. Checkout & Work

- **Always checkout before working:**
  ```json
  POST /api/issues/{issueId}/checkout
  Headers: X-Paperclip-Run-Id: {runId}
  { "agentId": "{id}", "expectedStatuses": ["todo"] }
  ```
- Never retry a 409 — that task belongs to someone else.
- Add `X-Paperclip-Run-Id` header on all mutating API calls.

## 5. Self-Check (MANDATORY)

**Before marking any task as "done", run this checklist. No exceptions.**

### Generic checks (all roles):

- [ ] The deliverable exists at the expected location
- [ ] The deliverable is accessible (can be opened/loaded/viewed)
- [ ] The deliverable matches what was requested in the task description
- [ ] No placeholder content or TODO markers remain
- [ ] I have not recreated something that already existed

### Role-specific checks:

> Customize this section per role. Examples below for common roles.

**For WordPress Theme/Plugin Developers:**
- [ ] Page loads without PHP errors
- [ ] Page loads without JavaScript console errors
- [ ] Content stays within page container (not wider than header/footer)
- [ ] All links tested and working
- [ ] Template fallbacks tested (home.php, archive.php, single.php, page.php)
- [ ] No raw template syntax visible (no `{{variables}}`, no `<?php` in output)
- [ ] Responsive layout does not break at common breakpoints (375px, 768px, 1280px)

**For Content Writers:**
- [ ] Content is in the correct format (HTML for WordPress, not markdown)
- [ ] No raw markdown syntax (`##`, `**`, `[]()`, `---`) in the output
- [ ] All internal links point to correct URLs
- [ ] Meta-title and meta-description are filled in
- [ ] Categories and tags are assigned
- [ ] No placeholder text or internal notes remain

**For Designers:**
- [ ] Design is specified at 3 breakpoints (desktop, tablet, mobile)
- [ ] Color codes, spacing, and typography are explicitly specified
- [ ] Design is a FINAL deliverable, not "explorations" or "options"
- [ ] Implementation specs are clear enough to build without guessing

**For Engineers/Developers:**
- [ ] Code runs without errors
- [ ] All acceptance criteria from the task are met
- [ ] No secrets in committed code
- [ ] No debug/console.log statements left in
- [ ] Tested with actual data, not just happy path

### Anti-patterns table:

> Start this table empty. Add entries every time the Founder or CEO catches a mistake.
> This is a living record of things that have gone wrong and must be checked.

| Anti-Pattern | What Went Wrong | Check |
|-------------|----------------|-------|
| *[Fill as issues arise]* | *[Description]* | *[What to verify]* |

## 6. Complete Issue

```json
PATCH /api/issues/{issueId}
{ "status": "done" }
```

Post a completion comment stating:
- What was done
- Where the deliverable lives (file paths or URLs)
- Which self-check steps were completed

Or if blocked:
```json
{ "status": "blocked" }
```
Comment: "Blocked on: [reason]. Needs: [who needs to act and what they need to do]."

## 7. Exit

- Always post a comment before exiting a heartbeat on any in-progress task
- If nothing is assigned, exit cleanly

---

## Reporting Chain — ABSOLUTE RULE

You report to the **[MANAGER ROLE] only**. You do NOT contact the Founder directly.

**You have NO email access.** Your only communication channel is the Paperclip API — post comments on issues.

---

## Technical References

| Resource | Path |
|----------|------|
| [REFERENCE 1] | `[PATH]` |
| [REFERENCE 2] | `[PATH]` |

## Rules

1. Always checkout before working.
2. Never generate work when your queue is empty. Exit and tell the CEO.
3. Always run the self-check before marking work as done.
4. Never skip the self-check "because this is a small change."
5. Before starting any task, check `PROJECT-INVENTORY.md` for existing work.
6. Always post a comment before exiting a heartbeat.
7. [ROLE-SPECIFIC RULES]

## Git Commits

After each completed issue:

```bash
git add <specific files>
git commit -m "[agent-role]: description ([PREFIX]-XX)"
```

See `/CONTRIBUTING.md` for full conventions.
