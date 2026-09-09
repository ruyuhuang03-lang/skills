---
name: project-status-manager
description: Create, read, and update a project's PROJECT_STATUS.md as a concise source of truth across Codex chats. Use when initializing project status tracking, recording progress or decisions, preparing a handoff, or grounding a new chat in the current state. Do not use it as a substitute for AGENTS.md rules or as a full chat transcript.
---

# Project Status Manager

Maintain a project-level `PROJECT_STATUS.md` that future chats can inspect directly.

## Separate rules from state

- Put durable instructions about how Codex should work in `AGENTS.md`.
- Put the project's current factual state in `PROJECT_STATUS.md`.
- Treat generated memories as a helpful recall layer, not as the authoritative project record.

When the project should use this workflow consistently, add a short rule to the applicable `AGENTS.md` requiring every project chat to read `PROJECT_STATUS.md` before work and, by default, update it after meaningful changes. Do not restrict writes to a project-control chat unless the user explicitly chooses that model.

## Resolve the project location

Before creating or changing the file, identify and report the exact project root or working directory. Respect an explicitly selected workspace. Place `PROJECT_STATUS.md` at the project root unless the user specifies another location.

Do not create or edit the file when the working directory is ambiguous. Do not overwrite an existing status file; read it and preserve valid user-authored content.

## Choose the operation

- **Initialize:** Create the file only when it is absent and the user wants status tracking set up.
- **Read:** Summarize the current goal, progress, decisions, blockers, and next actions without editing.
- **Update:** Patch only the sections affected by verified work or an explicit user decision.
- **Handoff:** Produce a compact handoff summary instead of writing when the user requests one, the chat lacks write access, or a concurrent edit cannot be merged safely.

## Initialize the status file

Use this structure, adapting sections to the project rather than filling them with invented content:

```markdown
# Project Status

Last updated: YYYY-MM-DD HH:MM TZ
Update policy: Project chats may update; project control resolves conflicts

## Goal

## Current phase

## Completed

## Key decisions

| Date | Decision | Rationale | Source chat or evidence |
|---|---|---|---|

## In progress

## Next actions

## Risks and blockers

## Latest handoff
```

Use the user's language for headings and prose. Omit empty optional sections when a smaller document is clearer.

When initializing a persistent workflow, add equivalent rules to the applicable `AGENTS.md`:

- Every project chat reads `PROJECT_STATUS.md` before starting substantive work.
- Every project chat updates it before finishing when the task produced verified progress, decisions, blockers, or next actions.
- A chat re-reads the latest file immediately before editing and preserves changes made by other chats.
- A chat must not overwrite an unresolved concurrent change; it returns a handoff for later merging instead.

## Update rules

1. Read the applicable `AGENTS.md`, the existing status file, and only the directly relevant project files before updating.
2. Record verified outcomes, explicit decisions, real blockers, and concrete next actions. Label uncertainty instead of presenting it as fact.
3. Keep entries concise. Do not copy full transcripts, long command output, chain-of-thought, credentials, tokens, or other secrets.
4. Mark work completed only after it is actually complete. Move stale items out of “In progress” and keep the current state internally consistent.
5. For a significant decision, record its date, rationale, and originating chat, issue, document, or file when available.
6. Update the timestamp using the user's or project's timezone. Preserve unrelated content and make a minimal patch.
7. Immediately before editing, re-read `PROJECT_STATUS.md` so the patch is based on the latest shared state.
8. After editing, review the resulting file and, in a Git repository, inspect the relevant diff when practical.

## Coordinate across chats

By default, every project chat may update `PROJECT_STATUS.md` after meaningful work. This is the normal mode and should not require the user to repeat an update prompt.

- Keep edits small and limited to the sections affected by the current task.
- If the file changed since it was first read, re-read it and merge the current task's update into the latest content once.
- If changes overlap, the correct merge is unclear, or another chat is actively writing, do not overwrite. Return a handoff containing completed work, key conclusions, decisions, changed files, remaining issues, and the recommended next action.
- A designated project-control chat resolves handoffs and conflicts; it is not the sole writer unless the user explicitly requests a single-writer workflow.

## Start and finish behavior

At the start of a task, summarize the status file briefly and call out missing or contradictory information that affects the request.

At the end, update `PROJECT_STATUS.md` without needing a repeated reminder when the task produced a meaningful state change and writing is safe. Otherwise leave it unchanged or return a handoff. State which outcome occurred, name the sections changed, and surface any unresolved blocker. Do not claim that chat memories, topics, or external documents were synchronized unless that action actually occurred.
