---
description: Save current session state to project memory for cross-session continuity
allowed-tools:
  - Bash
  - Read
---

# /pm:save - Persist Session Context

## Steps

### 1. Analyze Current Session

Before saving, identify:
- What tasks were worked on?
- What was accomplished?
- What's still in progress?

### 2. Save Session State

Read template from `${PLUGIN_ROOT}/templates/session.md`, fill placeholders:
- `{{datetime}}` - current datetime (YYYY-MM-DD HH:MM)
- `{{working_on}}` - tasks/tickets being worked on
- `{{progress}}` - what was accomplished
- `{{next}}` - what's remaining

Write to `active/sessions/current`.

### 3. Save/Update Task Progress (if applicable)

Read template from `${PLUGIN_ROOT}/templates/task.md`, fill placeholders:
- `{{ticket}}` - ticket ID (e.g., PROJ-123)
- `{{title}}` - brief description
- `{{status}}` - in_progress, blocked, review
- `{{done}}` - completed items (use `- [x]` format)
- `{{next}}` - remaining items (use `- [ ]` format)
- `{{files}}` - key file paths
- `{{datetime}}` - current datetime

Write to `active/tasks/TICKET-ID`.

### 4. Archive Completed Tasks (if any)

```bash
pm archive "active/tasks/TICKET-ID" --category completed
```

### 5. Save Learnings (if any discoveries)

Read template from `${PLUGIN_ROOT}/templates/learning.md`, fill placeholders:
- `{{title}}` - topic name
- `{{content}}` - what you learned and when it's useful
- `{{datetime}}` - current datetime

Write to `learnings/[topic]`.

### 6. Confirm

```bash
pm tree
pm stats
```

Report:
```
## Session Saved

**Updated:**
- active/sessions/current
- active/tasks/[ticket]

**Learnings:**
- learnings/[topic]

**Archived:**
- [completed tickets]

Ready for handoff.
```
