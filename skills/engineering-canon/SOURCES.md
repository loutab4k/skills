# Sources for `engineering-canon`

Every link in the four reference files, with its HTTP check and the phrase found in the downloaded content, plus the reuse limits per source. All 84 links returned 200 on 2026-10-17, and the 9 slop-indicator links in culture.md on 2026-10-30; use this file to re-check a link or a licence.

## Method

- Status: `curl -sSIL` on the URL without its `#` fragment. GitHub answered 429 (rate limit) to a few requests; each of those returned 200 on a second request.
- Content: the page or the raw file at the same pin was downloaded and the phrase below was found with `grep -iF` after joining lines and stripping HTML tags. Line anchors (`#L…`) point at the line where the phrase starts.
- Pins: GitHub links use a tag (`go1.26.0`, `v0.37.1`) or a 7-character commit SHA; the content check used the full SHA. Kernel docs are pinned to `v7.2`, LLVM docs to release `23.1.0`, PostgreSQL docs to `17`. Blog posts and postmortems are dated pages. Apple HIG, Telegram, the SRE book, the SWE book and AOSA have no versioned URL.
- Apple HIG pages render with JavaScript; their text was checked in the JSON the page loads (`developer.apple.com/tutorials/data/design/human-interface-guidelines/<page>.json`).
- Not verified anywhere: nothing. No principle was dropped for an unverifiable source.

## culture.md

| Ref | Status | Phrase found |
|---|---|---|
| ep-std | 200 | "definitely improves the overall code health" |
| ep-small | 200 | "one self-contained change" |
| ep-refac | 200 | "Separate Out Refactorings" |
| ep-desc | 200 | "Short summary of what is being done" |
| swe13 | 200 | "Prefer Realism Over Isolation"; "A fake is preferred over other test double techniques" |
| swe15 | 200 | "code is a liability, not an asset"; "orderly migration away from and eventual removal" |
| swe22 | 200 | "shards a master change into smaller pieces" |
| ted | 200 | "rewrite it so that a special case goes away and becomes the normal case" |
| mk | 200 | "special case goes away" |
| lwn | 200 | "Good programmers worry about data structures and their relationships" |
| k-fn | 200 | "Functions should be short and sweet, and do just one thing" |
| k-ind | 200 | "more than 3 levels of indentation" |
| k-exit | 200 | "Centralized exiting of functions" |
| k-sep | 200 | "Separate each logical change into a separate patch" |
| k-desc | 200 | "Describe your problem" |
| k-reg | 200 | "the \"no regressions\" rule" |
| ct | 200 | "Make the requirements less dumb"; "try very hard to delete the part or process"; "optimize something that should simply not exist"; "a person can" |
| iev | 200 | "MAKE THE REQUIREMENTS LESS DUMB"; "automated, accelerated, simplified and then deleted" |
| yt | 200 | page title "Starbase Tour with Elon Musk [PART 1 // Summer 2021]"; the spoken content was not checked |
| conn | 200 | "Connascent elements that are close together in a codebase are better than ones that are far apart" |
| scream | 200 | "not about the frameworks" |
| dup | 200 | "Two code fragments look almost identical" |
| eml | 200 | "Make illegal states unrepresentable" |
| lc | 200 | "A class contains many fields/methods/lines of code" |
| ss | 200 | "many small changes to many different classes" |
| clean | 200 | "source code dependencies can only point inwards" |
| mm | 200 | "delegating work to another class" |
| pdv | 200 | "Parse, don't validate" (the page uses a typographic apostrophe) |

## code.md

| Ref | Status | Phrase found |
|---|---|---|
| go-io | 200 | `type ReadWriter interface {` embedding `Reader` and `Writer` (lines 86–134) |
| go-hf | 200 | "The HandlerFunc type is an adapter to allow the use of" |
| go-pat | 200 | "Patterns can match the method, host and path"; `[METHOD ][HOST]/[PATH]` |
| go-err | 200 | "the %w verb to the error argument" |
| go-wrap | 200 | `func Is(err, target error) bool` |
| go-slog | 200 | "you can redact secret information like passwords" |
| go-guide | 200 | "it is better to produce some output, however imperfect, than to produce none at all" |
| go-sync | 200 | "Time in a bubble only advances when every goroutine in the bubble is durably blocked" |
| gs-least | 200 | "#### Least mechanism" |
| gs-err | 200 | "translate domain-specific errors into a standardized error space" |
| gs-if | 200 | "Avoid creating interfaces until a [real need]"; "Do not define back doors or export [test double] implementations" |
| gs-own | 200 | "The consumer defines the interface" |
| gs-pkg | 200 | "Avoid uninformative package names like `util`" |
| ll-exit | 200 | "Use Early Exits and continue to Simplify Code" |
| ll-else | 200 | "Don't use else after a return" |
| ll-layer | 200 | "should only use things from the libraries listed in its dependencies"; "no circular dependencies between libraries" |
| ll-assert | 200 | "Check all of your preconditions and assumptions" |
| ll-err | 200 | "Accidentally discarding an unchecked error will cause a program to abort" |
| aosa | 200 | "LLVM IR is both well specified and the only interface to the optimizer"; "library-based design" |
| mg-eng | 200 | file is 94 lines (`wc -l`) |
| nc | 200 | "no giant configuration objects, model factories, or if-then-else monsters" |
| kp-skel | 200 | "Set up the end-to-end training/evaluation skeleton + get dumb baselines"; "builds from simple to complex" |
| kp-data | 200 | "Become one with the data"; "The outliers especially almost always uncover some bugs" |

## product-contracts.md

| Ref | Status | Phrase found |
|---|---|---|
| hig-w | 200 | "Be action oriented."; "display it as close to the problem as possible, avoid blame" |
| hig-f | 200 | "a warning about possible data loss"; "Make sure all feedback is accessible." |
| hig-l | 200 | "Show something as soon as possible."; "Clearly communicate that content is loading and how long it might take" |
| hig-o | 200 | "fast, fun, and optional"; "Teach through interactivity." |
| hig-a | 200 | "Convey information with more than color alone."; "Strive to meet color contrast minimum standards." |
| swift | 200 | "Clarity at the point of use"; "Omit needless words" |
| swift-roles | 200 | "Name variables, parameters, and associated types according to their roles" |
| re-eff | 200 | "You don't need Effects to transform data for rendering"; "calculate it during rendering" |
| re-st | 200 | "Avoid contradictions in state"; "replace them with one `status` state variable" |
| re-red | 200 | "Reducers must be pure"; "Each action describes a single user interaction" |
| aip155 | 200 | "`string request_id`"; "Stale success responses" |
| aip193 | 200 | "The `reason` field is a short snake_case description"; "UPPER_SNAKE_CASE" |
| aip193m | 200 | "offer an actionable resolution" |
| aip158 | 200 | "Page tokens provided by APIs **must** be opaque"; "Adding pagination to an existing RPC is a backwards-incompatible change" |
| aip180 | 200 | "Existing client code **must not** be broken"; "New required fields **must not** be added"; "Default values must not change" |
| tg-upd | 200 | "An update is considered confirmed as soon as getUpdates is called with an offset higher than its update_id" |
| tg-wh | 200 | "X-Telegram-Bot-Api-Secret-Token" |
| tg-rp | 200 | "retry_after" |
| tg-faq | 200 | "avoid sending more than one message per second" |
| tg-init | 200 | "HMAC-SHA-256 signature of the data-check-string"; "check the auth_date field"; "Data from this field should not be trusted" |
| td-tl | 200 | file present at the pin (td/generate/scheme/td_api.tl) |
| td-gen | 200 | `tl-parser -e auto/tlo/td_api.tlo scheme/td_api.tl`; `generate_c.cpp`, `generate_java.cpp`, `generate_json.cpp` |

The Bot API page listed Bot API 10.3 as its latest version at check time.

## reliability.md

| Ref | Status | Phrase found |
|---|---|---|
| sre-gs | 200 | "The four golden signals of monitoring are latency, traffic, errors, and saturation" |
| sre-sym | 200 | "Symptoms Versus Causes"; "Every page should be actionable" |
| sre-retry | 200 | "per-request retry budget of up to three attempts"; "per-client retry budget" |
| sre-thr | 200 | "adaptive throttling"; "Requests above the cap fail locally" |
| sre-dl | 200 | "Deadline propagation"; "check that there is enough time left" |
| sre-shed | 200 | "Serve degraded results"; "Always use randomized exponential backoff" (same page) |
| br-idem | 200 | "An atomic phase is a set of local state mutations that occur in transactions between foreign state mutations"; `recovery_point` |
| br-drain | 200 | "A worker starts running it before its enclosing transaction is committed"; "staged in a table within the relational database" |
| pg-iso | 200 | "inconsistent snapshot"; "unsuitable for commands that involve complex search conditions"; "must be prepared to retry transactions due to serialization failures" |
| pg-dl | 200 | "acquire locks on multiple objects in a consistent order" |
| pg-skip | 200 | "Skipping locked rows provides an inconsistent view of the data" |
| cf25 | 200 | "doubled in size"; "Currently that limit is set to 200, well above our current use of ~60 features"; "called Result::unwrap() on an Err value"; "in the same way we would for user-generated input" |
| cf19 | 200 | "backtracked enormously and exhausted CPU"; "without a staged rollout"; "re2 or Rust regex engine which both have run-time guarantees" |
| wd | 200 | "uses capabilities instead of global namespaces"; "will never break your JavaScript code" |
| k-level | 200 | "the system's behavior is *level-based* rather than *edge-based*" |
| k-ctrl | 200 | "*desired state*"; "*current state*" |
| k-spec | 200 | "#### Spec and Status"; "**Conditions** provide a standard mechanism for higher-level status reporting" |
| k-cc | 200 | "resource versions* to achieve optimistic concurrency"; "the update fails with a StatusConflict" |
| k-pnw | 200 | `func (c *Controller) processNextWorkItem`; `c.workqueue.AddRateLimited(objRef)` |
| k-sync | 200 | "syncHandler compares the actual state with the desired, and attempts to converge the two" |

## Licences and reuse limits

| Source | Licence | Reuse in the canon |
|---|---|---|
| Google eng-practices, Go Style Guide | CC BY 3.0 (repo LICENSE) | Paraphrase plus link; short quotes with attribution allowed |
| Software Engineering at Google | CC BY-NC-ND 4.0 (page footer) | Paraphrase plus link; no adapted copies |
| Google SRE book | CC BY-NC-ND 4.0 (page footer) | Paraphrase plus link; no adapted copies |
| Google AIPs | CC BY 4.0 content, Apache-2.0 code samples (repo LICENSE) | Paraphrase plus link |
| Linux kernel docs | Kernel tree; per-file licence not checked | Paraphrase plus link |
| LWN article | "Copyright 2006, Eklektix" | Link only |
| TED talk transcript | "© TED Conferences, LLC. All rights reserved." | Link only |
| mkirchner write-up, micrograd, nanochat | MIT (GitHub licence) | Paraphrase plus link |
| Karpathy blog | No licence or copyright notice found on the page | Link only |
| CleanTechnica, InsideEVs, YouTube | Not checked; treat as publisher copyright | Link only; secondary sources for the five steps |
| Go stdlib, golang/example | BSD-3-Clause | Paraphrase plus link |
| LLVM docs | Apache-2.0 with LLVM Exceptions (`llvm/LICENSE.TXT` at `llvmorg-23.1.0`) | Paraphrase plus link |
| AOSA book | CC BY 3.0, stated on the aosabook.org index, not on the chapter page | Paraphrase plus link |
| Apple HIG | "Copyright © 2026 Apple Inc. All rights reserved." | Link only |
| Swift API Design Guidelines | Apache-2.0 (swift-org-website LICENSE) | Paraphrase plus link |
| React docs, Kubernetes website | CC BY 4.0 | Paraphrase plus link |
| Telegram Bot API and Mini Apps docs | No notice found on the pages; treat as Telegram copyright | Link only |
| TDLib | BSL-1.0 | Paraphrase plus link |
| connascence.io | CC BY-SA 3.0 (stated on the page) | Paraphrase plus link |
| Refactoring.Guru | "© 2014-2026 Refactoring.Guru. All rights reserved." | Link only |
| Clean Coder blog | No notice found on the pages | Link only |
| Jane Street blog | "© Copyright 2015-2026 Jane Street Group, LLC. All rights reserved." | Link only |
| Alexis King's blog | "© 2025, Alexis King" | Link only |
| Brandur Leach blog | No licence or copyright notice found on the pages | Link only |
| PostgreSQL 17 docs | PostgreSQL Licence (not re-checked here) | Paraphrase plus link |
| Cloudflare blog | No notice found for the post text; treat as Cloudflare copyright | Link only |
| workerd, Kubernetes community, sample-controller | Apache-2.0 | Paraphrase plus link |
