---
name: lock
description: Restore the project's default (prompting) permission settings after an unlocked session. Use when the user runs `/lock` or asks to re-enable permission prompts / reset permissions to default.
---

# lock

Reverses what `/unlock` did: restores [.claude/settings.json](.claude/settings.json) to its pre-unlock state so tool calls prompt for approval again.

## Process

1. **Read** [.claude/settings.json](.claude/settings.json).

2. **Restore from backup if present.**
   - If a top-level `_permissionsBackup` field exists, replace the current `permissions` object with it, then delete `_permissionsBackup`.
   - If no backup is present, fall back: remove `permissions.defaultMode` (if set) so the harness reverts to its built-in default. Leave the `allow` list as-is.

3. **Write** the file back with 2-space indentation.

4. **Tell the user:**
   - Default permissions are restored in settings.
   - **Takes effect in a new session** — the current session keeps whatever mode it started in. Restart to return to prompting behavior.
   - Confirm whether the restore came from `_permissionsBackup` or from the fallback (removing `defaultMode`), so they know what state the file is in.

## Do not

- Do not touch `~/.claude/settings.json`.
- Do not invent a new `allow` list — only restore from backup or leave the existing one alone.
