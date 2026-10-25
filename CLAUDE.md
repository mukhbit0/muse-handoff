# CLAUDE.md — muse-handoff

Claude Code reads this file automatically at the start of every session
connected to this repo. It tells you how to hand work to Goku, the user's
Muse agent, through this repo. No pasting needed in sessions on this repo.

## The handoff

Goku is the user's Muse agent. He lives on his own machine, has his own
memory, files, and connected accounts, and watches this repo for tasks.
Whenever the user asks you to hand work to Goku / delegate to Goku / ask
Goku to do something:

1. Pull the latest state of this repo first.
2. Write one task file at `tasks/inbox/YYYYMMDD-HHMMSS-<short-slug>.md`
   (date/time in Asia/Karachi, e.g. `20261026-044500-fix-seo-tags.md`).
3. Use this format exactly:

```markdown
---
id: <same as the filename without .md>
from: claude-code
created: <ISO timestamp with +05:00>
priority: normal
repo: <repo the work is about, or none>
---

## Task
What to do, in one paragraph.

## Context
Repo + branch, file paths, links, decisions already made. Goku cannot
see files on the user's machine, so put everything he needs here or
point at a repo he can pull.

## Done when
How to tell the task is finished. Be concrete.

## Limits
Anything Goku must NOT do.
```

4. Commit and push the file. Then tell the user it's queued — Goku
   usually picks it up within about a minute and reports back in the main
   chat, with the result in `tasks/done/<id>.md`.
5. Never ask Goku to publish, post, send email, spend money, or delete
   things by himself — he prepares that work and asks the user first.
6. One task per file. Be specific; if anything is unclear, ask the user
   instead of guessing.
7. To check what Goku finished, read `tasks/done/`.

## Repo rules

- Only touch `tasks/inbox/` for new tasks and `tasks/done/` to read
  results. Don't edit `HANDOFF.md`, this file, or the skill unless the
  user explicitly asks.
- Never push to any repo except this one from a handoff task.
- Full protocol: `HANDOFF.md`. Paste-ready prompt for sessions on other
  repos: `claude-web-prompt.md`.
