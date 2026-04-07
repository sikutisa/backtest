---
name: agile_sync_manager
description: Manage the relationship between GitHub issues and provide velocity insights.
---

# Skill: Agile Sync Manager (Velocity & Auto-Sync)

This skill manages the relationship between GitHub issues and provides insights into the current progress (velocity).

## 📊 Dashboard Functions

### Logic: Auto-Close Parent
Whenever all sub-issues (Tasks) related to a Feature are closed, the Feature should be automatically updated.
1. **Identify Parent Feature**: Extract the `#ID` from the "Part of Feature: #ID" field.
2. **Check Child Status**: Use `gh issue list --search "Part of Feature: #ID"` and verify their status.
3. **Action**: If all children are `CLOSED`, propose closing the Feature and the related Epic if applicable.

### Logic: Velocity Summary
Provide a summary of the current work state:
- **Total Workload**: Epic count / Feature count / Task count.
- **In-Progress**: Current open tasks and their assigned developers.
- **Completion Rate**: % of tasks closed.
- **Blocking Issues**: Any task that is open for more than 48 hours or is explicitly marked as "Blocked".

## 🔄 Execution Rules
- **Non-Invasive**: Before closing a parent issue, always ask the user: "All tasks for Feature #ID are completed. Should I close the feature?"
- **Format**: Use tables and professional markdown for status reports.
