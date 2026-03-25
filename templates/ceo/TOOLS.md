# CEO Tools — [COMPANY NAME]

## Paperclip API

Base URL: `http://localhost:3100/api`
Your agent ID: `[CEO_AGENT_ID]`
Company ID: `[COMPANY_ID]`

### Common endpoints

```bash
# Health check
GET /api/health

# Dashboard overview
GET /api/companies/{companyId}/dashboard

# Your assigned issues
GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress

# Issue checkout (ALWAYS do before starting work)
# X-Paperclip-Run-Id header is REQUIRED — server returns 401 without it
POST /api/issues/{issueId}/checkout
Headers: X-Paperclip-Run-Id: {runId}
Body: { "agentId": "{yourAgentId}", "expectedStatuses": ["todo", "backlog", "blocked"] }

# If issue is already in_progress (crash recovery):
Body: { "agentId": "{yourAgentId}", "expectedStatuses": ["in_progress"] }

# Complete an issue
PATCH /api/issues/{issueId}
Body: { "status": "done" }

# Post a comment
POST /api/issues/{issueId}/comments
Body: { "body": "markdown comment" }

# Create a subtask
POST /api/companies/{companyId}/issues
Body: { "title", "description", "parentId", "goalId", "projectId", "assigneeAgentId", "status": "todo" }

# Create agent via approval flow (recommended — Founder gets notified)
POST /api/companies/{companyId}/agent-hires
Body: { "name": "...", "role": "...", "reportsTo": "{managerAgentId}", "capabilities": "...", "budgetMonthlyCents": 5000 }

# Pause an agent (after task completion, no follow-up work)
POST /api/agents/{agentId}/pause

# Resume + wake an agent (when delegating new work)
POST /api/agents/{agentId}/resume
POST /api/agents/{agentId}/wakeup

# Goals
GET /api/companies/{companyId}/goals
PATCH /api/goals/{goalId} { "status": "achieved" }

# Projects
GET /api/companies/{companyId}/projects
POST /api/companies/{companyId}/projects { "name", "description", "goalIds", "status": "in_progress" }
```

## File System

- Company root: `[COMPANY_ROOT_PATH]`
- CEO home: `[COMPANY_ROOT_PATH]/agents/ceo/`
- Documentation: `[COMPANY_ROOT_PATH]/docs/`
- Agent configs: `[COMPANY_ROOT_PATH]/agents/`

## Email

Use **gogcli** (`/usr/local/bin/gog`) for all email actions.

### Reading incoming mail
```bash
# Search for Founder emails
gog gmail search 'from:[FOUNDER_EMAIL] label:[LABEL] is:unread' --max 10

# Check for replies in threads you started
gog gmail search 'label:[LABEL] in:inbox is:unread' --max 10

# Read a specific thread
gog gmail thread get <threadId>
```

### Sending email (ALWAYS gogcli, NEVER Gmail MCP)
```bash
/usr/local/bin/gog gmail send \
  --to [FOUNDER_EMAIL] \
  --subject "[PREFIX] Subject here" \
  --body "Message here" \
  --body-html "<p>HTML message here</p>"
```

- Subject ALWAYS starts with `[PREFIX]`
- NEVER use `gmail_create_draft` — send directly
