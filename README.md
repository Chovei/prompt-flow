# prompt-flow

A tiny Claude Code plugin for a workflow that gets better results and uses fewer tokens:

1. **Talk** about your idea and turn it into a detailed master prompt, right inside Claude (or in ChatGPT, if you prefer).
2. **Plan** it in Claude Code's plan mode before any code is written.
3. **Build** it in auto mode once the plan looks right.
4. **Hand off** to a fresh chat after each big project.

Small changes skip all of that: just ask directly.

## Install

In Claude Code:

```
/plugin marketplace add Chovei/prompt-flow
/plugin install prompt-flow@prompt-flow
```

Then restart Claude Code. To get updates later, run `/plugin marketplace update prompt-flow`.

## The commands

| When | Run | What happens |
|---|---|---|
| Starting something big, all in Claude | `/prompt-flow:idea <just talk>` | Asks you a few clickable questions, writes the master prompt and saves it to `docs/prompts/`. Reply **go** and it plans in plan mode. The interview runs on Sonnet to save usage; planning and building use your normal model. |
| Starting something big, prompt from ChatGPT | `/prompt-flow:master-prompt <paste prompt>` | Cleans up the prompt into Goal / Features / Constraints / Out of scope / Done when, saves it to `docs/prompts/`, switches to plan mode and plans. Approve the plan, switch to auto mode, done. |
| A small change | `/prompt-flow:quick <what to change>` | No planning. Smallest possible change, quick check, 2-3 line report. Stops and tells you if it's bigger than it looks. |
| Finished a big piece of work | `/prompt-flow:handoff` | Writes `HANDOFF.md`: what was done, decisions, what's open, next steps, how to run it. |
| Starting the new chat | `/prompt-flow:resume` | Reads `HANDOFF.md` and tells you where things stand in a few lines. |

## Stay in Claude

Type `/prompt-flow:idea `, then just talk: press **Win+H** on Windows (or **Fn Fn** on Mac) to dictate into Claude's input box. Ramble as much as you like. Claude reads it, asks a few multiple-choice questions you can click (or type your own answer), and writes the master prompt for you.

## Or use ChatGPT for the interview

If you want the interview to cost zero Claude usage, set up a ChatGPT Project with the instructions in [`chatgpt/prompt-builder.md`](chatgpt/prompt-builder.md). Open it, talk, answer its questions, and paste the prompt it gives you after `/prompt-flow:master-prompt`.

## Tips

- **Plan mode and auto mode:** press **Shift+Tab** to cycle modes in Claude Code.
- **Run `/init` once per project** to create a `CLAUDE.md`, then add the section from [`templates/CLAUDE-workflow-section.md`](templates/CLAUDE-workflow-section.md). Claude reads it every chat, so you stop repeating yourself.
- **New chat per big project.** Long chats get slower, pricier and fuzzier. `handoff` + `resume` make switching painless.

## License

MIT
