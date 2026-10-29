# Culture: review, changes, design taste

How strong teams review, size and describe changes, and decide what to build or delete. Read it when you plan a change, write a commit or PR, or review one.

Entry format and precedence: [SKILL.md](SKILL.md).

## Google Engineering Practices

- **Approve once the change clearly improves code health.** Perfect is not the bar. Supports: core.md › Development cycle, step 5. [standard.md][ep-std]
- **One change does one self-contained thing.** Keep refactoring apart from behaviour changes. Supports: core.md › Scope (design commit before the behaviour change) and › Engineering (related changes as separate commits in one PR; the owner's form wins over Google's separate CL). [small-cls.md][ep-small], [refactorings][ep-refac]
- **The first line says what the change does; the body says why.** Supports: the `report-writing` skill › Shape (open with what changed and why). [cl-descriptions.md][ep-desc]

## Software Engineering at Google (ch. 13, 15, 22)

- **Prefer real implementations over test doubles.** A fake comes before a mock. Supports: engineering.md › Checks and tests (E2E without test doubles first). [ch. 13][swe13]
- **Code is a liability.** Deprecation is planned work: migrate the callers, then remove the old system. Supports: engineering.md › Design (parts replaceable and removable); core.md › Engineering (delete what has no consumer). [ch. 15][swe15]
- **Split a large change into shards.** Each shard is tested, reviewed and submitted on its own, driven by tooling. Supports: core.md › Engineering (automate repeated steps; risky changes get their own PR). [ch. 22][swe22]

## Linus Torvalds

- **Good taste: rewrite the code so the special case disappears.** The edge case becomes the normal case. Supports: engineering.md › Design (make invalid states unrepresentable). [TED transcript][ted], [annotated example][mk]
- **Design the data structures first.** Good code follows from data and its relationships. Supports: engineering.md › Design (domain types). [LWN, 2006][lwn]
- **Functions are short and do one thing.** More than three levels of indentation means split it. Use one exit path for cleanup. Supports: no owner rule; advisory. [functions][k-fn], [indentation][k-ind], [central exit][k-exit]
- **One logical change per patch.** The message describes the problem first. Supports: core.md › Engineering (separate commits). [separate changes][k-sep], [describe changes][k-desc]
- **No regressions.** What worked for a user keeps working after an upgrade. Supports: engineering.md › Invariants 2 (a shared contract evolves as a whole); neither owner doc has an explicit compatibility rule. [regressions rule][k-reg]

## SpaceX / Elon Musk: the five steps

Secondary-sourced: Musk said it on camera in 2021; the wording below follows two write-ups of that interview, not an official SpaceX text.

- **1. Make each requirement less dumb.** Every requirement has a named person as its owner, and a smart person's requirement gets questioned too. Supports: core.md › Scope (propose a better approach). [CleanTechnica][ct], [InsideEVs][iev]
- **2. Delete the part or process.** If nothing ever has to be added back, too little was deleted. Supports: core.md › Engineering (delete code, flags and shims without a consumer). Limit: engineering.md forbids mass deletion of useful tests. [CleanTechnica][ct]
- **3. Simplify and optimise only what survived.** The common mistake is optimising something that should not exist. Supports: core.md › Engineering (smallest amount of good code). [CleanTechnica][ct]
- **4–5. Speed up the cycle, then automate, in that order.** Automating a step you should have deleted is waste. Supports: core.md › Engineering (automate every repeated step, after steps 1–3). [InsideEVs][iev], [video][yt]

## Slop indicators

Nine signs that a codebase is decaying, as a checklist for a review or an audit (the list follows a post by @mazeincoding on X, 2026-10-29; each sign links a primary source instead).

- **Implicit coupling.** Two parts must change together, but nothing in the code says so: a shared magic value, an order of calls, a timing. The farther apart they sit, the worse. Supports: engineering.md › Design (another module's state only through its public contract). [connascence.io][conn]
- **Layer-first folders.** The top-level folders name layers (`controllers/`, `services/`, `models/`), so one feature is spread over all of them. Folders that name the domain show what the system does. Supports: no owner rule; advisory. [Screaming Architecture][scream]
- **Duplication.** The same rule, threshold or format lives in two places and drifts. Supports: engineering.md › Invariants 2 (one owner per piece of knowledge); core.md › Engineering (delete copies). [Duplicate Code][dup]
- **Representable illegal states.** The types allow a combination the domain forbids, so every reader must guard against it. Supports: engineering.md › Design (make invalid states unrepresentable). [Effective ML][eml]
- **God files.** One file holds many responsibilities and grows with every change. Supports: engineering.md › File size (move one whole responsibility out). [Large Class][lc]
- **Shotgun surgery.** One change needs small edits in many files. Gather that knowledge in one owner. Supports: engineering.md › Invariants 1 (consolidate the scattered logic you touch). [Shotgun Surgery][ss]
- **Layering violations.** An inner layer imports an outer one: the domain knows about HTTP, the UI computes prices. Dependencies point inwards. Supports: engineering.md › Design (HTTP, UI and templates stay in adapters) and › Invariants 3 (presentation only displays). [The Clean Architecture][clean]
- **Pass-through wrappers.** A function or class only forwards to another and adds nothing, so the reader learns two interfaces for one behaviour. Supports: core.md › Scope (deeper modules, simpler interfaces); details in `mattpocock-codebase-design`. [Middle Man][mm]
- **Errors and validation away from the boundary.** Input is checked deep inside and again in several places, instead of being parsed once at the edge into a type that cannot be wrong. Supports: core.md › Engineering (check a fact once at its boundary and trust it inside). [Parse, don't validate][pdv]

[ep-std]: https://github.com/google/eng-practices/blob/3bb3ec2/review/reviewer/standard.md#L31
[ep-small]: https://github.com/google/eng-practices/blob/3bb3ec2/review/developer/small-cls.md#L46
[ep-refac]: https://github.com/google/eng-practices/blob/3bb3ec2/review/developer/small-cls.md#L175
[ep-desc]: https://github.com/google/eng-practices/blob/3bb3ec2/review/developer/cl-descriptions.md#L34
[swe13]: https://abseil.io/resources/swe-book/html/ch13.html#prefer_realism_over_isolation
[swe15]: https://abseil.io/resources/swe-book/html/ch15.html
[swe22]: https://abseil.io/resources/swe-book/html/ch22.html#sharding_and_submitting
[ted]: https://www.ted.com/talks/linus_torvalds_the_mind_behind_linux/transcript
[mk]: https://github.com/mkirchner/linked-list-good-taste/blob/cbc3fb9/README.md
[lwn]: https://lwn.net/Articles/193245/
[k-fn]: https://www.kernel.org/doc/html/v7.2/process/coding-style.html#functions
[k-ind]: https://www.kernel.org/doc/html/v7.2/process/coding-style.html#indentation
[k-exit]: https://www.kernel.org/doc/html/v7.2/process/coding-style.html#centralized-exiting-of-functions
[k-sep]: https://www.kernel.org/doc/html/v7.2/process/submitting-patches.html#separate-your-changes
[k-desc]: https://www.kernel.org/doc/html/v7.2/process/submitting-patches.html#describe-your-changes
[k-reg]: https://www.kernel.org/doc/html/v7.2/admin-guide/reporting-regressions.html#what-is-a-regression-and-what-is-the-no-regressions-rule
[ct]: https://cleantechnica.com/2021/08/16/elon-musk-reveals-his-5-step-engineering-protocol/
[iev]: https://insideevs.com/news/526954/elon-musk-5-steps-success/
[yt]: https://www.youtube.com/watch?v=t705r8ICkRw
[conn]: https://connascence.io/
[scream]: https://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html
[dup]: https://refactoring.guru/smells/duplicate-code
[eml]: https://blog.janestreet.com/effective-ml-revisited/
[lc]: https://refactoring.guru/smells/large-class
[ss]: https://refactoring.guru/smells/shotgun-surgery
[clean]: https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[mm]: https://refactoring.guru/smells/middle-man
[pdv]: https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/
