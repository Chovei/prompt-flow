---
name: quick
description: Make a small, focused change without plan mode - read only what's needed, change as little as possible, check it, report briefly.
argument-hint: <the small change you want>
disable-model-invocation: true
---

# Quick change

The user wants a small change, with no planning step:

<change>
$ARGUMENTS
</change>

If the request is empty, ask what they want changed and stop.

## How to work

1. **Don't enter plan mode** and don't write a plan.
2. Find the right place fast: search for the relevant names or text and read only the files you need. Don't explore the whole project.
3. Make the **smallest change** that does what was asked. Match the surrounding code style. Don't refactor, rename or "improve" anything that wasn't asked for.
4. If the project has an obvious quick check for what you touched (a test file, a lint or type check, a build), run just that. Skip it if there isn't one.
5. Report in 2–3 lines: what changed (with file paths), and whether the check passed.

## Stop if it's not small

If, once you look, the change needs a design decision, touches many files, or would take more than a handful of edits, **stop before editing**. Say in two lines why it's bigger than it looks, and suggest running `/prompt-flow:master-prompt` with a short description instead.
