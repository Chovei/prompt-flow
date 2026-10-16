# CLAUDE.md workflow section

Claude Code reads `CLAUDE.md` at the start of every chat. Run the built-in `/init` once in your project to create one, then paste this section at the bottom:

```markdown
## Workflow
- Big features and first implementations come in through /prompt-flow:master-prompt and are planned in plan mode before any code is written.
- Small changes come in through /prompt-flow:quick: change as little as possible, no refactors that weren't asked for.
- If HANDOFF.md exists, it describes the latest state of the project. Prefer it over guessing.
- Saved master prompts live in docs/prompts/.
```

Add your own project rules under it (how to run tests, code style, things never to touch). Every line you put here is a line you never have to type again.
