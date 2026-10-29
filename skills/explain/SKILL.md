---
name: explain
description: Explain a topic, a codebase area or an agent's output in the form the reader takes in fastest, from plain text to an interactive page.
disable-model-invocation: true
argument-hint: "The topic, file or output to explain"
---

# Explain

1. Read the source first: the code, doc, log or output the explanation covers, never memory.
2. Pick the lowest rung that carries the point, and name it in one line:
   1. text, written as the reply rules say;
   2. a static `.html` diagram: one idea per panel, real names and numbers from the source, colour that means something;
   3. an interactive `.html` page, only when the reader changes an input and sees the result, with the real algorithm running in the page.
3. Write a page to the scratchpad, or to `.claude/reports/` when the owner keeps it. A page stays a local file; publish it as an Artifact only when the owner wants to show it to someone, with their yes.
4. Compare the result with the source and restore every fact, number and condition the simplification dropped.
5. Check a page as the reply rules say, then give its absolute path and offer the next rung in one line.

Done when every fact of the source that the explanation touches survives in it, a page renders clean at desktop width and at 375 px, and the reply names the rung and offers the next one.
