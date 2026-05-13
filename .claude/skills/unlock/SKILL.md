---
name: unlock
description: Switch the project into full-permission (bypass) mode so long unattended runs (e.g. overnight research loops) don't pause for approval prompts. Use when the user runs `/unlock` or asks to disable permission prompts for the session.
---

# unlock

Edits [.claude/settings.json](.claude/settings.json) to set `permissions.defaultMode` to `"bypassPermissions"`, so every tool call is auto-approved.

## Process

1. **Read** [.claude/settings.json](.claude/settings.json).

2. **Back up the current `permissions` object** by writing it verbatim into a top-level `_permissionsBackup` field in the same file. This is what `/lock` will restore. If `_permissionsBackup` already exists, leave it alone — the user is unlocking an already-unlocked-ish state and we don't want to overwrite the true default.

3. **Set** `permissions.defaultMode` to `"bypassPermissions"`. Leave the existing `allow` list untouched (it's harmless in bypass mode and becomes the fallback if the mode is removed).

4. **Write** the file back with 2-space indentation.

5. **Tell the user, clearly:**
   - Full-permission mode is written to settings.
   - **It only takes effect in a new session.** They must exit this session and start a fresh one (or reload) for prompts to stop.
   - Remind them to run `/lock` when they're done to restore the safe default.
   - Warn once: in bypass mode every tool call runs without asking, including bash and writes anywhere on disk. Only use it for trusted unattended work.

## Do not

- Do not edit `~/.claude/settings.json` (the global one) — only the project file.
- Do not delete or rewrite the `allow` list.
- Do not claim the change is "active now" — it is not, until session restart.
