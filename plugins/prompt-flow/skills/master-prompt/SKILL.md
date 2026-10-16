---
name: master-prompt
description: Turn a pasted master prompt (or a rough spoken ramble) into a saved, structured prompt, then plan the work in plan mode before building anything.
argument-hint: <paste your master prompt or describe what you want>
disable-model-invocation: true
---

# Master prompt → plan

The user wants to start a big piece of work (a new feature, a first implementation, a rework). Their input:

<input>
$ARGUMENTS
</input>

If the input is empty, ask the user to paste their master prompt (or just describe what they want) and stop. If they'd rather talk it through, suggest `/prompt-flow:idea` instead.

If the input is a path to an existing `.md` file (for example one saved by `/prompt-flow:idea` in `docs/prompts/`), read that file and use its contents as the input. It's already saved, so skip step 2's saving.

## 1. Shape the prompt

The input may already be a structured master prompt (for example one written by ChatGPT), or it may be a rough, rambling description dictated by voice. Either way, end up with a prompt in exactly these sections:

```markdown
# <short title>

## Goal
<one or two sentences: what this builds and why>

## Features
- <each thing it must do, concrete and testable>

## Constraints
- <tech stack, style, things to keep, performance, platforms>

## Out of scope
- <what NOT to build now>

## Done when
- <how we will know it works: what to run, see or click>
```

Rules:
- Keep the user's intent and wording where you can. Don't invent features they didn't ask for. Put your own ideas under a separate `## Suggestions (not yet agreed)` section at the end, if any.
- Look at the project briefly (README, CLAUDE.md, package files, folder layout) so Constraints match what is really there.
- Ask **at most 3** short questions, and only when the answer would change the plan (for example: which framework, where it should live, what "done" looks like). If nothing important is missing, ask nothing.

## 2. Save it

- If you are **not** in plan mode: save the prompt to `docs/prompts/<YYYY-MM-DD>-<short-slug>.md` in the project (create the folder if needed). Tell the user the path in one line.
- If you are **already** in plan mode: don't create the file. Put the full prompt at the top of the plan instead, under `## Master prompt`.

## 3. Plan

- If you are not in plan mode yet, call the `EnterPlanMode` tool now (load it with ToolSearch first if it is listed only as a deferred tool). If that tool is not available, tell the user to press **Shift+Tab** until plan mode is on and run the command again.
- Explore the code the plan touches, then write a plan that covers every item in **Features** and **Done when**, in small steps, smallest working version first. Name the files you will change and how you will test.
- Present the plan for approval. Don't write code before the user approves it.

## 4. After approval

Tell the user in one line: "Switch to auto mode (Shift+Tab) if you want me to build it without asking at every step." Then build the plan.

When the work is done and tested, suggest `/prompt-flow:handoff` before they start their next big task in a new chat.
