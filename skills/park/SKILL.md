---
name: park
description: Checkpoint all work so the next session resumes instead of redoing it. Use when the owner says "паркуйся" or "park", or before the work moves to a new session.
---

# Park

Parking leaves each piece of work at a **checkpoint** the next session resumes from without asking the owner: committed or listed changes, a current status note, and a resume step for every child. It has two branches:

- **Shutdown:** the owner says «паркуйся» or "park" before shutting the device down. A shutdown kills every running session, child and background command on the device. Run all four steps, then stop.
- **Handoff:** the work moves to a new session, because the context nears its limit or the owner asks. This session's context does not reach the next one: wait for running children to finish before the note, so the next session reads their results instead of starting a second implementer. Run all four steps, with the handoff in step 4, then give the owner the status note's path and end the turn.

## 1. Stop starting work

From now on launch no child, command or edit beyond the steps below. A child that receives "park" runs this skill itself and returns its park report to its parent.

## 2. Checkpoint the changes

For each checkout you edited in this session:

- When the task or project grants commit permission and the checkout is on your own branch (never the default branch), stage only the files you changed that had no uncommitted changes before you edited them (`git add <path>…`, never `-A` or `.`) and commit them as `WIP: <slice> — <what is unfinished>`. Leave the commit local, and list every other file you changed instead of committing it.
- Otherwise, or when the commit fails, commit nothing and list the checkout, its branch and each file you changed.
- Leave files you did not change as they are, the owner's uncommitted edits included.

Done when every checkout you touched has a WIP commit or a file list.

## 3. List the running work

List every piece of work still running, each with its resume step. In a handoff, children have finished (the handoff branch above waits for them) and only background commands may still run: record those the same way, and the resume step is what the next session does.

| Kind | Record | Resume after the restart |
|---|---|---|
| Child (Agent tool) | agent id or name, its task | in the same session resumed, `SendMessage` to the same agent, which keeps its history; Explore and Plan agents are one-shot, and an agent from another session is lost: run those again |
| Background command or Monitor | the exact command line, its output file | the shutdown ends it: check whether its effect landed (its output file, `git log`, `gh run view`); rerun in the background only a command that is safe to repeat, otherwise ask the owner |

Done when every child you launched and every background command you started in this session is in the table or known to have ended.

## 4. Update the status note

Write into the project's status note (`.local-status.md`, `JOURNAL.md` or the file the project names):

- **Shutdown:** the goal, the state of each slice, the table from step 3, and the next step. Then report the same to the owner and end the turn.
- **Handoff:** a handoff that lets a fresh session continue without asking the owner:
  - the goal;
  - the current state: branch, PR, what passes and what fails;
  - decisions with their reasons;
  - open questions and blockers;
  - next steps in order;
  - each finished child's result, or where it is;
  - the table from step 3.

  Link specs, PRs and commits instead of copying them, and write no secrets. Give the owner the status note's path; the next session reads the note first.
