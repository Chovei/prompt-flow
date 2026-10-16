---
name: idea
description: Stay in Claude for the whole big-task flow - talk about what you want, answer a few clickable questions, get a saved master prompt, then reply go to plan it.
argument-hint: <just talk about what you want to build>
model: sonnet
disable-model-invocation: true
---

# Idea → interview → master prompt

The user wants to start a big piece of work and would rather talk than write a prompt. Their input, often dictated and messy:

<input>
$ARGUMENTS
</input>

If the input is empty, ask one open question and wait: "What do you want to build? Just talk; on Windows, Win+H lets you dictate." Then continue with their answer.

## 1. Understand

- Read the whole input and pull out what they want, even if it's out of order or repeats itself.
- Look at the project briefly (README, CLAUDE.md, package or config files, top-level folders) so your questions and the Constraints fit what's really there. Don't read source files in depth yet.

## 2. Interview with clickable questions

Use the **AskUserQuestion** tool (load it with ToolSearch first if it's listed only as a deferred tool). If it isn't available, ask the same questions as a short numbered list instead.

- Ask **at most 4 questions per round, and at most 2 rounds.** Stop as soon as nothing important is open.
- Ask only what changes the result: scope (what's in the first version), where it lives, tech or style, what "done" looks like, what to leave out.
- Give each question **2–4 concrete options**, recommended one first with "(Recommended)" in its label. Never add an "Other" option, because the user can always type their own answer.
- Don't ask what the input or the project already answers.
- If an answer is free text, use it as given: it may be a wish or a fact rather than one of your options. Never treat it as picking your recommended option.

## 3. Write the master prompt

Use exactly these sections:

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

- Keep the user's intent and wording. Don't add features they didn't ask for. Put your own ideas under `## Suggestions (not yet agreed)` at the end.
- Save it to `docs/prompts/<YYYY-MM-DD>-<short-slug>.md` (create the folder if needed).
- Show the prompt, then say: **"Saved to `<path>`. Reply go to plan it, or tell me what to change."**

Stop there. Don't plan or write code in this turn.

## 4. When the user replies

- **"go" (or a yes):** call the `EnterPlanMode` tool (load it with ToolSearch if it's deferred; if it's unavailable, ask the user to press Shift+Tab until plan mode is on). Read the saved prompt file and plan from it: cover every Feature and Done when item, in small steps, smallest working version first. Name the files you'll change and how you'll test. Present the plan for approval. After approval, say in one line: "Switch to auto mode (Shift+Tab) if you want me to build it without asking at every step."
- **Changes:** update the saved file, show what changed, and ask for "go" again.
