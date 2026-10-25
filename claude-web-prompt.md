# For Claude on the web (claude.ai/code)

**You usually don't need this file anymore.** The same instructions now
live in `CLAUDE.md` at the repo root, which Claude Code reads automatically
at the start of every session connected to this repo.

Use this file only for sessions on *other* repos, where the handoff
repo's CLAUDE.md isn't loaded. Paste the short pointer below once at the
start of such a session:

> To delegate to Goku (the user's Muse agent): write a task file in the
> private repo mukhbit0/muse-handoff at
> `tasks/inbox/YYYYMMDD-HHMMSS-<short-slug>.md` (Asia/Karachi time), with
> frontmatter `id / from: claude-code / created / priority / repo` and
> sections `Task / Context / Done when / Limits`. Full format:
> mukhbit0/muse-handoff/CLAUDE.md. Commit and push. Goku picks it up
> within about a minute and reports back in the main chat; results land
> in `tasks/done/`. Never ask him to publish, send, spend, or delete
> anything by himself.

Full prompt (only if the short pointer isn't enough — e.g. a fresh
session that has never seen the handoff format):

---

You are working with Goku, the user's Muse agent, through a shared private
repo: mukhbit0/muse-handoff.

Goku watches that repo and does tasks left for him there. Whenever I ask
you to hand work to Goku / delegate to Goku / ask Goku to do something:

1. Make sure this repo (mukhbit0/muse-handoff) is connected to this
   session, and pull the latest state first.
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
see files on my machine, so put everything he needs here or point at a
repo he can pull.

## Done when
How to tell the task is finished. Be concrete.

## Limits
Anything Goku must NOT do.
```

4. Commit and push the file. Then tell me it's queued — Goku usually
   picks it up within about a minute and reports back in the main chat,
   with the result in `tasks/done/<id>.md`.
5. Never ask Goku to publish, post, send email, spend money, or delete
   things by himself — he prepares that work and asks me first.
6. One task per file. Be specific; if anything is unclear, ask me
   instead of guessing.
7. To check what Goku finished, read `tasks/done/`.

If this repo isn't connected to this session, stop and tell me to connect
mukhbit0/muse-handoff first — don't pretend you wrote the file.

---

## Note: plain claude.ai chat can't do this

The plain claude.ai chat's GitHub integration is read-only — it reads file
names and contents only. It can draft a task file for you, but it cannot
push it to the repo. For that, use Claude Code on the web (claude.ai/code)
with the prompt above, or paste the drafted file into the repo yourself
on github.com (Add file → commit) — Goku picks it up from there the same way.
