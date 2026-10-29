---
name: report-writing
description: How to write a PR description, report, doc, issue or commit message for its reader. Use before writing or editing one.
---

# Report writing

The owner's rules for any text a person reads later: a PR description, a report, a doc, an issue or a commit message. Briefs and messages to other agents, the status note and the mistakes log keep their own form.

If a `BINDINGS.md` sits next to this file, read it first: it names this host's files, checks and tools for this skill.

## Shape

- Open with what changed or was found and why, in one or two sentences; a doc opens with what it covers and when to use it.
- Group the rest by topic, under short headings when there is more than one topic: one idea per bullet, at most two levels.
- Keep only what the reader needs to act or trust the result. Leave out process history (review rounds, attempts, interim CI states, timestamps; a one-line "test fails without the fix" is evidence, not history) and repeats across sections.
- Give evidence as one line per claim: the command and its result, or a link. Run each evidence line on the final tree before publishing it, and quote what it searched for exactly as you ran it.
- Write a doc for the merged state; a one-time post-merge step goes to the PR's post-merge list.

## PR description

Write it in the `mattpocock-pr` skill's sections (Summary, Evidence, Merge Danger), with these rules:

- Open with the result. When more than five files change, add the **reading order**: which files to read first and which changes are mechanical.
- Summary: a sketch of the mechanism (a diff sketch, pseudocode or a call tree) for a change to logic; a removal or a rename gets a short list instead.
- Evidence: each acceptance criterion with its one-line evidence. A behaviour change also shows **before** (the base) and **after** (the branch) for one scenario: test names, output or a manual run. Longer evidence goes to a linked review comment or report.
- Merge Danger: **Door** (one-way or two-way, naming the live steps to reverse), **Blast Radius**, **Known limits** and **Left out** when there are any, and **Failure detection**: how a failure after merge would be noticed (a check, a hook refusal, a log, or "silent").
- The free text stays within about 250 words; the template's own text, the sketch, the evidence and Merge Danger do not count. Count the words before publishing.

## Project templates

A project template wins over these rules: keep every field it requires, one line each, including process fields such as Independent review (reviewer, given, findings, fixes, re-review result), with a link to the full review.

Completion criterion: the text opens with the result, every claim has its one-line evidence, and a PR description has its reading order when more than five files change, its sketch or list, its criteria, before and after for a behaviour change, and its Door, Blast Radius and Failure detection lines, with the free text within its budget.
