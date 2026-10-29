# Code: shape, errors, interfaces

Code to imitate when you write or review Go or shape any module: packages, interfaces, errors, logging, concurrency tests.

Entry format and precedence: [SKILL.md](SKILL.md).

## Go standard library at go1.26.0

- **Small interfaces, composed.** `Reader` and `Writer` have one method each; `ReadWriter` only embeds them. Supports: engineering.md › Design (reach a module through its public contract). [io.go][go-io]
- **HTTP is a thin adapter.** A one-method `Handler`, the `HandlerFunc` adapter and `ServeMux` method-and-path patterns; no framework. Supports: engineering.md › Design (HTTP stays in adapters). [HandlerFunc][go-hf], [patterns][go-pat]
- **Wrap with `%w` and inspect with `errors.Is`/`errors.As`.** The cause stays reachable through the chain. Supports: engineering.md › Design (keep error causes). [errors.go][go-err], [wrap.go][go-wrap]
- **Logs never fail and never leak.** `LogValue` redacts a secret at its type; a handler prints something on bad input rather than erroring. Supports: core.md › Permissions (secrets never printed). [slog doc][go-slog], [handler guide: robustness][go-guide]
- **Test timers and workers with `testing/synctest`.** A bubble's fake clock advances only when all its goroutines are durably blocked; no sleeps. Supports: no owner rule; advisory. [synctest.go][go-sync]

## Google Go Style Guide

- **Least mechanism.** Use the most standard tool that works; added complexity is hard to remove later. Supports: core.md › Engineering (smallest amount of good code). [guide][gs-least]
- **Wrap with `%w` inside the system; translate at its edges.** At RPC or storage boundaries, map errors to a canonical error space. Supports: engineering.md › Design (keep error causes; HTTP in adapters). [best practices][gs-err]
- **No interface before a real need; the consumer defines it.** Do not export test doubles; test through the real public API. Supports: core.md › Engineering (delete what has no consumer); engineering.md › Checks and tests. [decisions][gs-if], [ownership][gs-own]
- **No `util`, `common` or `helper` packages.** Name a package for what it owns. Supports: engineering.md › Invariants 1 (one owning module per domain). [decisions][gs-pkg]

## LLVM: Coding Standards (release 23.1.0) and Lattner's AOSA chapter

- **Exit early.** Guard clauses and `continue` cut nesting; no `else` after `return`. Supports: no owner rule; advisory. [early exits][ll-exit], [else after return][ll-else]
- **Layer libraries without cycles.** A library uses only the libraries it declares. Supports: engineering.md › Invariants 1 (an import that works around a cycle means the boundaries need fixing). [library layering][ll-layer]
- **Assert internal invariants; never drop a recoverable error.** LLVM's `Error` aborts if left unchecked. Supports: engineering.md › Refactoring and enforcement (lock rules into CI). Limit: asserts do not replace the one check at the boundary (core.md › Engineering). [assert liberally][ll-assert], [recoverable errors][ll-err]
- **One well-specified IR is the only contract between parts.** Front ends and optimisers know only the IR; each part is a library a client picks or replaces. Supports: engineering.md › Design (public contract; parts replaceable). [AOSA ch. 11][aosa]

## Andrej Karpathy

Imitate the shape, not the Python idioms.

- **A complete core in one small file.** micrograd's whole autograd engine is 94 lines. Supports: core.md › Engineering (smallest amount of good code). [engine.py][mg-eng]
- **No framework machinery.** One cohesive code base with no giant config objects, factories or long if-else chains. Supports: core.md › Engineering (delete flags and shims without a consumer). [nanochat README][nc]
- **End-to-end skeleton first, then add complexity in verified steps.** Start with dumb baselines; each step tests one hypothesis. Supports: core.md › Development cycle, step 3 (one slice at a time). [Recipe, step 2][kp-skel]
- **Look at the real data before you build on it.** Outliers reveal bugs in data and preprocessing. Supports: engineering.md › Checks and tests (golden tests on real inputs and edge cases). [Recipe, step 1][kp-data]

[go-io]: https://github.com/golang/go/blob/go1.26.0/src/io/io.go#L86-L134
[go-hf]: https://github.com/golang/go/blob/go1.26.0/src/net/http/server.go#L2278-L2282
[go-pat]: https://github.com/golang/go/blob/go1.26.0/src/net/http/server.go#L2463-L2476
[go-err]: https://github.com/golang/go/blob/go1.26.0/src/errors/errors.go#L19-L25
[go-wrap]: https://github.com/golang/go/blob/go1.26.0/src/errors/wrap.go#L45
[go-slog]: https://github.com/golang/go/blob/go1.26.0/src/log/slog/doc.go#L217-L220
[go-guide]: https://github.com/golang/example/blob/7f05d21/slog-handler-guide/README.md#L854-L866
[go-sync]: https://github.com/golang/go/blob/go1.26.0/src/testing/synctest/synctest.go
[gs-least]: https://github.com/google/styleguide/blob/b2a398d/go/guide.md#L184-L190
[gs-err]: https://github.com/google/styleguide/blob/b2a398d/go/best-practices.md#L924-L1018
[gs-if]: https://github.com/google/styleguide/blob/b2a398d/go/decisions.md#L2216-L2232
[gs-own]: https://github.com/google/styleguide/blob/b2a398d/go/best-practices.md#L3733-L3745
[gs-pkg]: https://github.com/google/styleguide/blob/b2a398d/go/decisions.md#L117
[ll-exit]: https://releases.llvm.org/23.1.0/docs/CodingStandards.html#use-early-exits-and-continue-to-simplify-code
[ll-else]: https://releases.llvm.org/23.1.0/docs/CodingStandards.html#don-t-use-else-after-a-return
[ll-layer]: https://releases.llvm.org/23.1.0/docs/CodingStandards.html#library-layering
[ll-assert]: https://releases.llvm.org/23.1.0/docs/CodingStandards.html#assert-liberally
[ll-err]: https://releases.llvm.org/23.1.0/docs/ProgrammersManual.html#recoverable-errors
[aosa]: https://aosabook.org/en/v1/llvm.html
[mg-eng]: https://github.com/karpathy/micrograd/blob/7bc720e/micrograd/engine.py
[nc]: https://github.com/karpathy/nanochat/blob/92d63d4/README.md
[kp-skel]: https://karpathy.github.io/2019/04/25/recipe/#2-set-up-the-end-to-end-trainingevaluation-skeleton--get-dumb-baselines
[kp-data]: https://karpathy.github.io/2019/04/25/recipe/#1-become-one-with-the-data
