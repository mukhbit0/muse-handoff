---
name: delegate-to-goku
description: Hand a task to Goku, the user's Muse agent, through the shared muse-handoff repo. Use when the user asks to give work to Goku/Muse, delegate something, or hand a task off.
---

# Delegate to Goku

Goku is the user's Muse agent. He lives on his own machine, has his own
memory, files, and connected accounts, and usually notices a new task
within about a minute of it landing in the handoff repo.

## When to use this

Only when the user asks to hand work to Goku, or when a task clearly belongs
to him (his files, his accounts, his pipelines) rather than to this session.
Never delegate silently: tell the user what you handed off and that Goku
will report back in the main chat.

## How to hand off

1. Make sure this machine has a clone of the handoff repo (clone once):
   `git clone git@github.com:mukhbit0/muse-handoff.git`
2. In that clone, `git pull`.
3. Copy `tasks/TEMPLATE.md` to
   `tasks/inbox/YYYYMMDD-HHMMSS-<short-slug>.md` (local time, Asia/Karachi)
   and fill it in:
   - **Task**: what to do, in one paragraph.
   - **Context**: repo + branch, file paths, links, decisions already made.
     Goku cannot see files on this Windows machine — put the context in the
     file or point at a repo he can pull.
   - **Done when**: concrete finish condition.
   - **Limits**: anything he must not do.
4. Commit and push.
5. Tell the user the task is queued and Goku will report back in the main
   chat, with the result also written to `tasks/done/<id>.md`.

## Rules

- One task per file. Be specific — vague tasks come back as questions.
- Never ask Goku to publish, post, send email, spend money, or delete
  things by himself. He prepares that work and asks the user first.
- If the user wants a reply from Goku sooner than a couple of minutes,
  say so: he can ask Goku directly in chat to check the inbox now.
- Check `tasks/done/` for results when the user asks what Goku finished.
