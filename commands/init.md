---
description: Initialize CLAUDE.md memory structure for project with interactive wizard
---

Initialize auto-managed CLAUDE.md memory files for this project.

## Workflow

### Step 1: Configure Trigger Mode

Ask the user how auto-memory should trigger updates using AskUserQuestion:

**Question**: "How should auto-memory trigger CLAUDE.md updates?"

**Options**:
- **default** (recommended): Track file edits in real-time. Updates trigger after Edit/Write operations and file modifications (rm, mv, etc.). Best for most workflows.
- **gitmode**: Only trigger on git commits. Updates happen when you commit changes. Best for developers who commit frequently and prefer "if you didn't commit, it didn't happen" workflow.

Save the selection to `.claude/auto-memory/config.json`:
```json
{
  "triggerMode": "default"
}
```

### Step 1b: Configure Auto-Commit (Optional)

Ask the user if they want CLAUDE.md changes auto-committed using AskUserQuestion:

**Question**: "Should auto-memory automatically commit CLAUDE.md changes after updates?"

**Options**:
- **No** (default): CLAUDE.md changes remain as local modifications. You commit them manually.
- **Yes**: Automatically commit CLAUDE.md files after each memory update. Commit message: `chore: update CLAUDE.md [auto-memory]`

If the user selects Yes, also ask about auto-push:

**Question**: "Should auto-memory also push CLAUDE.md commits to the remote?"

**Options**:
- **No** (default): Commits stay local until you push manually.
- **Yes**: Automatically push after each auto-commit.

Update `.claude/auto-memory/config.json` with the selections:
```json
{
  "triggerMode": "default",
  "autoCommit": false,
  "autoPush": false
}
```

### Step 1c: Update .gitignore

Also ensure `.gitignore` includes the dirty-files tracking files:
1. Check if `.gitignore` exists in the project root
2. If it exists, check if it already contains `.claude/auto-memory/dirty-files*`
3. If not present, append the entries under a `# Claude Code auto-memory` comment section
4. If `.gitignore` doesn't exist, create it with the entries

Example addition to `.gitignore`:
```
# Claude Code auto-memory
.claude/auto-memory/dirty-files*
```

Note: The wildcard pattern covers both the legacy `dirty-files` and session-specific `dirty-files-{session_id}` files.

### Step 2: Analyze Codebase

Invoke the `codebase-analyzer` skill to:
1. Analyze the codebase structure
2. Detect frameworks and build commands
3. Identify subtree candidates for monorepos
4. Detect code patterns and conventions

### Step 3: Generate CLAUDE.md

Guide the user through the setup process and confirm before writing any files.
