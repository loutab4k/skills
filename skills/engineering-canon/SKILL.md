---
name: engineering-canon
description: Owner-chosen exemplars and principles, with links. Use when designing or reviewing a module, API, schema, worker, bot flow or UI flow.
---

# Engineering canon

Principles from sources the owner chose, each tied to the owner rule it supports and linked to a pinned source. Use it to sharpen a design or a review with a concrete exemplar.

If a `BINDINGS.md` sits next to this file, read it first: it names this host's files, checks and tools for this skill.

## When to use

- You design or review a module, package, API, schema, transaction, worker, queue, bot flow or UI flow.
- You need an exemplar or a reason behind an owner rule.
- Skip it for routine edits that touch none of these.

## Read only the matching file

| Task | File |
|---|---|
| Plan, size or describe a change; review a diff; decide what to delete; check a codebase for slop | [culture.md](culture.md) |
| Package and interface shape, errors, logging, Go code, concurrency tests | [code.md](code.md) |
| UI copy, feedback and state; HTTP API contract and errors; Telegram bots and Mini Apps | [product-contracts.md](product-contracts.md) |
| Monitoring, retries, overload, transactions and locks, outbox, config rollout, reconcile loops | [reliability.md](reliability.md) |

Each entry: the principle in our words, then "Supports:" with the owner rule it backs (`engineering.md` for the owner's engineering rules, `core.md` for the core rules, then the section) or "no owner rule; advisory", then pinned links. Link checks and licences are in [SOURCES.md](SOURCES.md); read it only to re-check a link.

## How to cite

- Paraphrase in your own words and give the link. Never paste long quotes.
- Name the source with the principle, e.g. "Go style: the consumer defines the interface (link)".
- Several sources limit reuse (Apple, Telegram, Cloudflare, SRE book, SWE book, LWN, TED). Link and paraphrase only.

## Precedence

- Binding owner rules win: the core rules (`core.md`), the engineering rules (`engineering.md`) and the project's own rules.
- The canon never adds a binding rule. It explains and illustrates; a finding that rests only on the canon is advisory.
- Where a canon principle conflicts with an owner rule, its entry names the limit. Follow the owner rule.
- Topics already covered by installed skills stay there: deep modules (`mattpocock-codebase-design`), Apple motion and typography (`emilkowalski-apple-design`).
