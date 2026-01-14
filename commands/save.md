---
description: Save current session state to project memory for cross-session continuity
allowed-tools:
  - Bash
---

# /pm:save - Persist Session Context

## Steps

### 1. Analyze Current Session

Before saving, identify:
- What tasks were worked on?
- What was accomplished?
- What's still in progress?

### 2. Save Session State

```bash
pm write "active/sessions/current" "## Session: $(date '+%Y-%m-%d')

### Working On
- [task/ticket]

### Progress
- [what was done]

### Next
- [what's remaining]
"
```

### 3. Save/Update Task Progress (if applicable)

```bash
pm write "active/tasks/TICKET-ID" "## TICKET-ID: [title]

### Status: in_progress

### Done
- [x] Completed step

### Next
- [ ] Remaining step

### Key Files
- [paths]
"
```

### 4. Archive Completed Tasks (if any)

```bash
pm archive "active/tasks/TICKET-ID" --category completed
```

### 5. Save Learnings (if any discoveries)

```bash
pm write "learnings/[topic]" "## [Topic]

[what you learned and when it's useful]
"
```

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

**Archived:**
- [completed tickets]

Ready for handoff.
```
