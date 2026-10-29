# Agent-system vocabulary

The words of the owner's agent setup: who works, how work is handed over and remembered, and how a change is verified, reviewed and reported. The always-loaded core glossary, where the host has one, holds the short form of the most used terms; this file holds every term in full. Sources: the core rules, the engineering rules, the routing rules, the `park` skill and the `mistakes-log` and `report-writing` skills.

## Language

### People and agents

**Owner**:
The person these rules serve: the one who asks, decides forks and grants permissions.
_Avoid_: user (for the owner); "user" stays for a product's users and Claude Code's own scopes (user settings)

**Session**:
One Claude Code conversation, from its start to its end.
_Avoid_: thread (a thread is a comment thread), project thread, chat

**Main session**:
The session the owner talks to; it plans, delegates, integrates and reports.
_Avoid_: main agent, main loop

**Child**:
An agent a session launches with the Agent tool, in a fresh context, for one slice or question; it launches none of its own and returns a report to its parent.
_Avoid_: subagent, sub-agent, worker; Claude Code's own names (`subagent_type`, `SubagentStop`) stay as they are

**Parent**:
The session that launched a child and receives its report.
_Avoid_: caller, orchestrator

**Implementer**:
The one child or session that writes a slice's code.
_Avoid_: coder, worker

**Reviewer**:
The fresh-context child that reviews one round of a change; never its implementer.
_Avoid_: critical reviewer (critical names a tier, not a role)

**Analyst**:
The read-only child launched on escalation; it returns an analysis and a plan and edits nothing.
_Avoid_: escalation child, Fable analyst

**Profile**:
A named child configuration with a default model and effort.
_Avoid_: agent type, persona

**Task class**:
A row of the routing table that maps a kind of task to a child's model and effort.
_Avoid_: task category, task type

**Escalation**:
Moving a problem one step up the routing ladder after its attempts fail, ending with the owner.
_Avoid_: return to the main agent, bump

### Work and handover

**Task**:
What the owner asked for; it may hold several slices.
_Avoid_: job, ticket (unless a tracker issue is meant)

**Slice**:
Our unit of work: one session or child, one implementer, with its progress in the status note and WIP commits.
_Avoid_: piece of work; in a testing context the word is **vertical slice** ([testing.md](testing.md))

**Brief**:
What a child or a new session is given to work from: objective, context, edit boundaries, permissions, expected result and checks.
_Avoid_: prompt, handoff, instructions

**Report**:
What a child returns to its parent: results with evidence, changed files, checks run, open questions.
_Avoid_: handoff, summary

**Handoff**:
Moving the work to a new session through the status note, with the `park` skill.
_Avoid_: handover; handoff for a child's report or for a brief

**Checkpoint**:
The state the next session resumes from without asking the owner: committed or listed changes, a current status note, a resume step for every running child.
_Avoid_: snapshot, save point

**WIP commit**:
A local commit on your own branch that saves a slice's unfinished progress between sessions.
_Avoid_: temp commit, savepoint

**Fork**:
A decision point where the viable options differ in behaviour, cost or risk, or where the choice is the owner's.
_Avoid_: open question (when options exist); a forked session is a Claude Code fork, a different thing

**Owner decision**:
A decision the owner made: a standing line in the owner's decisions file, or one a brief passes with how long it holds (this PR, this task or standing).
_Avoid_: approval (a yes to one action), policy

### Memory

**Status note**:
The project's file that holds the current state of the work: goal, decisions, blockers and next step. It is `.local-status.md`, `JOURNAL.md` or the file the project names.
_Avoid_: journal, handoff note, notes file

**Mistakes log**:
The project's `AGENT_LEARNINGS.md`: one lesson per confirmed agent mistake, read before work.
_Avoid_: learnings, agent log, lessons file

**Lesson**:
One entry of the mistakes log: a trigger, a rule, its evidence and what enforces it.
_Avoid_: learning; lesson for a general rule (that is a pattern)

**Trigger**:
The situation an entry's `## When …` heading names; an entry is read when its trigger matches the task.
_Avoid_: tag, category

**Pattern**:
A general rule kept from retired lessons in `guards-and-patterns.md`; it still binds new code after its entry is gone.
_Avoid_: lesson (for these rules), best practice

### Development cycle

**Acceptance criterion**:
A task's checkable "input -> expected result" pair, written before work into the status note and later into the PR.
_Avoid_: done criterion, "Done when" (for a task), requirement

**Completion criterion**:
The condition that ends one step of a skill or a doc, written as "Done when …".
_Avoid_: acceptance criterion (that is per task)

**Design up front**:
The design written into the status note before code, point by point as engineering.md lists them.
_Avoid_: spec, plan (committed files of their own)

**Self-check**:
The evidence list written after the checks: sources, `rg` sweeps, edge inputs, a mutation check per criterion, script runs, a stale-docs sweep.
_Avoid_: self-review, self-test

**Review tier**:
The level of review the riskiest part of a diff sets: self-review, ordinary or critical.
_Avoid_: review level; "critical" for anything but this tier and a task class

**Self-review**:
The lowest tier's review of your own diff against the review checklist, with each criterion's one-line evidence.
_Avoid_: self-check

**Review round**:
One reviewer's pass over a change: round 1 reviews in depth, later rounds only verify the fixes.
_Avoid_: fix round, iteration

**Findings ledger**:
The record of a review's findings, each marked fixed or rejected with its evidence.
_Avoid_: ledger (unqualified), review notes

**Comment test**:
The bar every code comment meets, engineering.md Design: a comment stays only when both clearly hold: it explains what we cannot change, and the next agent would otherwise spend several tool calls to learn it; a surprise in our own code is fixed in the code instead. A reviewer checks it on each comment a diff adds or changes.
_Avoid_: comment policy, comment rule

**Finding label**:
The reviewer's bucket for a finding: defect (wrong in a real case, fixed now), text (a comment, doc or name) or beyond (outside the change, a tracker issue).
_Avoid_: severity, nit

**Not verified**:
The label of a claim that cannot be checked now, given with the reason and the source.
_Avoid_: unverified, assumed, probably

**Not run**:
The label of a step or check that was not executed, written `not run: <reason>`.
_Avoid_: skipped

**Not done**:
The label of requested work left unfinished.
_Avoid_: partial, pending (a status word of its own)

The testing terms of the cycle (mutation check, snapshot test, golden test) live in [testing.md](testing.md); the gate and the base check in [git-ci.md](git-ci.md).

### Reports and pull requests

**Merge Danger**:
The PR section on what a merge risks: Door, Blast Radius, Known limits, Left out and Failure detection.
_Avoid_: risks, caveats

**Door**:
A PR's reversibility: one-way or two-way, naming the live steps that reverse it. The word is used only for PRs.
_Avoid_: door for a hook event (Claude Code's mods name that field `door`; the docs say hook event)

**Blast Radius**:
What a failure after the merge can reach.
_Avoid_: impact, scope

**Failure detection**:
How a failure after the merge would be noticed: a check, a hook refusal, a log line, or silent.
_Avoid_: monitoring, alerting

### Guards and safety

**Hook**:
Code the harness runs at a hook event.
_Avoid_: plugin, script (when the hook is meant)

**Hook event**:
The point in a session at which a hook runs, such as a tool call, a tool result or a reply.
_Avoid_: door, trigger

**Guard**:
A hook or check that refuses or asks, and never grants.
_Avoid_: filter, gate (the gate is the project's checks)

**Matcher**:
The pattern inside a guard that decides what it refuses.
_Avoid_: rule, regex (when the guard's pattern is meant)

**Masked value**:
A private value that a tool result shows as `<masked:kind>` instead of the value itself.
_Avoid_: secret (not every masked value is one), redacted value

**Scratchpad**:
The per-session temporary directory Claude Code assigns; deleting entries inside it needs no permission.
_Avoid_: tmp, scratch dir
