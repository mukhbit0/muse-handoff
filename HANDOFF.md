# muse-handoff — Claude Code ⇄ Goku (Muse)

Private task channel between Claude Code (on Mukhbit's Windows machine) and
Goku, his Muse agent. Claude drops a task file in `tasks/inbox/`; Goku
usually picks it up within about a minute.

## Flow

1. **Claude** (or Mukhbit, by hand): pull latest, copy `tasks/TEMPLATE.md`
   into `tasks/inbox/` as `YYYYMMDD-HHMMSS-<short-slug>.md`, fill it in,
   commit, push.
2. **Goku**: an instant watcher notices a new file within about a minute
   (a 5-minute scheduled check runs as backup). For each new task it does
   the work, appends a `## Result` section, moves the file to
   `tasks/done/`, commits, pushes, and tells Mukhbit in the main chat.
3. **Claude** (or Mukhbit): read the result in `tasks/done/<id>.md`.

## Task file format

One task per file. Frontmatter first, then sections:

```markdown
---
id: 20261026-0430-fix-seo-tags
from: claude-code
created: 2026-10-26T04:30:00+05:00
priority: normal   # low | normal | high
repo: mukhbit0/yt_automation   # or "none"
---

## Task
What to do, in one paragraph.

## Context
Links, file paths, branch names, decisions already made — everything
Goku needs so he doesn't have to ask.

## Done when
How to tell the task is finished. Be concrete.

## Limits
Anything Goku must NOT do (e.g. "don't publish", "don't touch main").
```

## Rules for Claude

- Be specific: vague tasks come back as questions instead of work.
- Goku cannot see files on the Windows machine. Put the context in the
  task, or point at a repo + branch he can pull.
- Never ask Goku to publish, post, send email, spend money, or delete
  things on his own. He will prepare the work and ask Mukhbit first.
- One task per file. If a task depends on another, say so in Context.

## Rules for Goku

- Only act on files in `tasks/inbox/`. Ignore anything else in this repo
  except the protocol files.
- Work the task, then move it to `tasks/done/` with a `## Result` section
  (what was done, file/commit links, what still needs Mukhbit).
- If a task asks to publish, send, spend, or delete: prepare it, do not
  execute it, and ask Mukhbit.
- If a task is unclear, ask Mukhbit in the main chat instead of guessing.
- Never push to any repo except this one.

## Claude-side setup (Windows)

```powershell
git clone git@github.com:mukhbit0/muse-handoff.git
xcopy skills\delegate-to-goku %USERPROFILE%\.claude\skills\delegate-to-goku\ /E /I
```

Then tell Claude Code: "delegate to Goku" — the skill in
`skills/delegate-to-goku/SKILL.md` teaches it the format above. Or just say
in chat: "write a task for Goku in muse-handoff about …".

## Claude on the web

- **Claude Code on the web (claude.ai/code):** connect this repo to the
  session. The instructions now live in `CLAUDE.md` at the repo root,
  which Claude Code reads automatically at the start of every session on
  this repo — no pasting needed. In sessions on *other* repos, paste the
  short pointer from `claude-web-prompt.md` once.
- **Plain claude.ai chat:** its GitHub integration is read-only — it can
  read the repo and draft a task file, but it cannot push one. Either use
  Claude Code on the web, or paste the drafted file into the repo
  yourself on github.com (Add file → commit). Goku picks it up the same way.
