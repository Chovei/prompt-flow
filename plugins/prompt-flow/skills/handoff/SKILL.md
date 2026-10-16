---
name: handoff
description: Before switching to a new chat, write HANDOFF.md so the next chat can pick up the project without re-explaining everything.
argument-hint: [optional notes to include]
disable-model-invocation: true
---

# Handoff

The user finished a big piece of work and wants to start a fresh chat (fresh chats are cheaper and sharper than very long ones). Write a handoff file the next chat can read in seconds.

Extra notes from the user, if any:

<notes>
$ARGUMENTS
</notes>

## 1. Gather

Use what you already know from this conversation first. Only look at files or `git status` / `git log -5 --oneline` if you need to confirm something. Don't re-read the whole project.

## 2. Write `HANDOFF.md` in the project root

Keep it short, about one screen. Facts only, no filler:

```markdown
# Handoff - <YYYY-MM-DD>

## What this project is
<one or two sentences>

## What was just done
- <the work finished in this chat, with key file paths>

## Decisions made
- <choices the next chat should not re-argue, and why in a few words>

## Not done / open
- <unfinished items, known bugs, things not tested>

## Next steps
1. <the most useful next thing to do>

## How to run and test
- <exact commands>

## Previous handoffs
- <YYYY-MM-DD: one-line summary>
```

If `HANDOFF.md` already exists, replace it, but keep its "Previous handoffs" list and add the old handoff's date and a one-line summary to the top of that list (keep at most 10 lines).

Don't put passwords, API keys, tokens or other secrets in the file.

## 3. Tell the user

In two lines: that `HANDOFF.md` is written, and to **start a new chat and run `/prompt-flow:resume`** there.
