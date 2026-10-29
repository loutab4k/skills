---
name: mistakes-log
description: Record a confirmed agent mistake in the mistakes log, with its entry format, repeat rule, caps and retirement. Use when evidence or the owner confirms a mistake, or before editing the log.
---

# Mistakes log

The agent mistakes log turns each confirmed mistake into a **lesson** the next run reads before it starts. It is `docs/agents/AGENT_LEARNINGS.md` where that file exists, otherwise `AGENT_LEARNINGS.md` next to the status note, created on the first entry. The core rules say when to read it.

If a `BINDINGS.md` sits next to this file, read it first: it names this host's files, checks and tools for this skill.

## Record a confirmed mistake

Record it in the same task, before the final reply; a remark from the owner confirms a mistake too.

1. Find the entry whose trigger covers the situation: `rg -n '^## When' <log>`. When one does, the mistake is a **repeat**: go to step 3.
2. Add one entry of at most 6 lines:
   - a `## When <situation>` heading: the trigger, the situation the next agent will be in;
   - the rule, in one line;
   - `Evidence:`, in one line or a link;
   - `Enforced by:`, last, naming the check, test or hook that refuses the mistake, or `judgment`.
3. A repeat goes into the existing entry (its rule and its `Evidence:` line), never as a new paragraph. A repeated `judgment` entry needs a check, or the owner's decision to keep judgment written on its `Enforced by:` line, as in `judgment (repeated, owner decision 10-25)` or ``judgment (repeated); `tests/x.sh` covers it``.

Done when the entry has its heading, rule, `Evidence:` and `Enforced by:` lines within 6 lines, and the log stays within its caps below.

## Keep the log small

- Delete an entry once a merged check refuses its mistake. When its rule holds a general pattern beyond the logged case, move that pattern in the same commit to the project's patterns doc instead of dropping it: retiring makes room, it does not forget.
- Rewrite or delete an entry whose rule proved wrong or out of date (the code, tool or rule it names changed), with that evidence in the commit: a stale lesson misleads every run that reads it.
- Keep the log within 300 lines and 20,000 bytes (about 5k tokens, one Read) by merging or retiring entries; never delete the log itself.
