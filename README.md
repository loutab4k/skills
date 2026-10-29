# Skills

[![skills.sh](https://skills.sh/b/loutab4k/skills)](https://skills.sh/loutab4k/skills)

Skills for working with a coding agent as a colleague you can trust: results written for their reader, one word per concept, a lesson from every confirmed mistake, procedures rehearsed before they are handed over, and work checkpointed so the next session resumes instead of redoing it.

They grew out of daily work with Claude Code. In the skills, "the owner" is the person the agent works for.

## Install

```bash
npx skills@latest add loutab4k/skills
```

## Why use it?

- **Fewer claims to re-check.** Reports open with the result and give one line of evidence per claim; procedures arrive with their rehearsal output.
- **Mistakes stop repeating.** Each confirmed mistake becomes a short lesson the next run reads first, and the log stays small enough to read in one go.
- **Less drift between sessions.** A checkpoint before a session ends and one canonical vocabulary keep the next session where the last one stopped.
- **Principles with sources.** The engineering canon ties each principle to a pinned, link-checked source.

## Host bindings

Five skills read an optional `BINDINGS.md` next to their `SKILL.md`. Put your own paths, checks and tools there, and the published text stays generic. This repo never ships a `BINDINGS.md`.

Some skills name skills by other authors with an author prefix, such as `mattpocock-pr`; install those separately.

## Reference

- **[engineering-canon](./skills/engineering-canon/SKILL.md)** — chosen engineering exemplars and principles with pinned links, for designing or reviewing a module, API, schema, worker or UI flow.
- **[explain](./skills/explain/SKILL.md)** — explains a topic, a codebase area or an agent's output in the form the reader takes in fastest, from plain text to an interactive page.
- **[glossary](./skills/glossary/SKILL.md)** — canonical words for the agent setup, UI, testing and Git and CI, each with the words to avoid.
- **[mistakes-log](./skills/mistakes-log/SKILL.md)** — turns each confirmed agent mistake into a short lesson, with its format, repeat rule, caps and retirement.
- **[owner-procedure](./skills/owner-procedure/SKILL.md)** — rehearses a multi-step procedure before handing it to the owner to run, and marks each step that could not run.
- **[park](./skills/park/SKILL.md)** — checkpoints all work so the next session resumes instead of redoing it.
- **[product-thinking](./skills/product-thinking/SKILL.md)** — a hard-question interview on a product idea that ends in build, don't build or test first.
- **[report-writing](./skills/report-writing/SKILL.md)** — PR descriptions, reports, docs, issues and commit messages written result first for their reader.
