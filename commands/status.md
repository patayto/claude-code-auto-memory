---
description: Show CLAUDE.md memory sync status
---

Display the current status of CLAUDE.md memory synchronization.

Check and report:
1. **Pending changes**: Count of files in `.claude/auto-memory/dirty-files` (or session-specific `dirty-files-*` files) awaiting processing
2. **Last sync**: Modification timestamp of CLAUDE.md
3. **CLAUDE.md locations**: All CLAUDE.md files found in the project
4. **Configuration**: Current trigger mode, autoCommit, and autoPush settings from `.claude/auto-memory/config.json`

If there are pending changes, offer to run `/auto-memory:calibrate` to process them.
