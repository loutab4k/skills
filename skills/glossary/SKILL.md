---
name: glossary
description: The owner's canonical words, each with the words to avoid. Use when naming a UI element, a test kind, a Git or CI operation or an agent-setup term, or when adding or changing a term.
---

# Glossary

One canonical word per concept, so a request, the reply and the code name the same thing. The always-loaded core glossary, where the host has one, holds the short form of the agent-setup words; these files hold every area in full.

If a `BINDINGS.md` sits next to this file, read it first: it names this host's files, checks and tools for this skill.

| File | Area |
|---|---|
| [agent-system.md](agent-system.md) | roles, handover, memory, development cycle, review, reports, guards |
| [ui-layout.md](ui-layout.md) | layout and spacing, typography, color and surface |
| [ui-components.md](ui-components.md) | overlays, menus, messages, disclosure, controls |
| [ui-interaction.md](ui-interaction.md) | states, navigation and scroll, forms, motion beyond Emil's, accessibility |
| [testing.md](testing.md) | test doubles, scope and size, oracles, reliability, mutation, TDD rhythm |
| [git-ci.md](git-ci.md) | undoing changes, history and merges, merge requirements, CI, releases |

Other skills own these vocabularies; use their terms as they define them: `mattpocock-codebase-design` (module, interface, seam, adapter, depth), `emilkowalski-animation-vocabulary` (motion), `mattpocock-tdd` (vertical slice, tracer bullet).

## Name a thing

Find what you see or mean in the area file and use its canonical term in the reply, the code and the docs. When a description fits two neighbouring terms, name both and say how they differ. A word under `_Avoid_` is not used for that entry's concept, except as a quoted external name, such as a product's, a tool's or a library's own term.

## Add or change a term

Add or change a term the moment it is settled, with the discipline of `mattpocock-domain-modeling`: one canonical term, its synonyms under `_Avoid_`, a definition of what the term is, no implementation detail, in that skill's GLOSSARY-FORMAT.md. A term lives in one area file only; a term another skill owns is referenced, never redefined, or, where the name is shared, its entry names the owning skill.

A rename also updates, in the same change, every rule text that uses the old word (instructions, docs, skills, output style), found with `rg -n -i '<old word>'`. A changed core term changes the core glossary too.

An owner-coined name with no other sense goes, once retired, into the host's list of retired words, where a check has one, so the check refuses it in any rule text from then on.

Done when the term sits in one area file, the core agrees with it, the sweep for each retired word finds only its `_Avoid_` line or a quoted external name, and the host's glossary check, if any, passes.
