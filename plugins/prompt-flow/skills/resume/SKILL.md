---
name: resume
description: Start a new chat from the last handoff - read HANDOFF.md, summarize where the project stands, and ask what's next.
disable-model-invocation: true
---

# Resume from handoff

This is a fresh chat picking up a project.

1. Read `HANDOFF.md` in the project root. If it doesn't exist, say so in one line, suggest running `/prompt-flow:handoff` at the end of the next big task, and stop.
2. If `CLAUDE.md` exists, read it too. Don't read anything else yet.
3. Reply with a short summary (5 lines at most): what the project is, what was done last, what's open, and the suggested next step.
4. Ask what they want to do next. Don't start any work until they answer.
