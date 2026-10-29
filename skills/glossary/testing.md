# Testing vocabulary

Words for asking an agent for a specific kind of test, test double or verification step. Terms owned by `mattpocock-codebase-design` (**module**, **interface**, **seam**, **adapter**, **depth**) and by `mattpocock-tdd` (**vertical slice**, **tracer bullet**, red → green, implementation-coupled and tautological tests) are used as defined there and not repeated. In a testing context say **vertical slice** in full: a bare slice is a unit of agent work ([agent-system.md](agent-system.md)).

## Language

### Test doubles

Source: Meszaros, xUnit Test Patterns, via https://martinfowler.com/bliki/TestDouble.html and http://xunitpatterns.com/SUT.html; mock vs stub: https://martinfowler.com/articles/mocksArentStubs.html

**System under test (SUT)**:
Whatever the test is verifying, defined from the test's point of view: a function, a module or the whole application.
_Avoid_: CUT, AUT, target, subject

**Depended-on component**:
A collaborator the SUT uses that this test is not verifying; the thing a test double replaces.
_Avoid_: dependency (fine in prose, but ambiguous with package dependencies), collaborator

**Test double**:
Any object that stands in for a depended-on component in a test. This is the generic word.
_Avoid_: mock (as a generic word), fake (as a generic word), stand-in

**Dummy**:
A test double that is passed only to fill a parameter and is never used.
_Avoid_: placeholder, null object

**Stub**:
A test double that returns pre-programmed answers and checks nothing about how it was called.
_Avoid_: mock, canned response

**Spy**:
A stub that also records the calls it received, so the test can assert on them afterwards.
_Avoid_: mock, recorder

**Mock**:
A test double that is set up with expected calls and fails the test when the calls differ. `mattpocock-tdd` and `mattpocock-codebase-design` say mock for any test double; read it there as test double.
_Avoid_: using "mock" for stubs, fakes or doubles in general

**Fake**:
A test double with a working but simplified implementation that is unfit for production, such as an in-memory repository. In `mattpocock-codebase-design` terms it is an in-memory **adapter**.
_Avoid_: mock, in-memory mock, mock adapter

**State verification**:
Asserting on the SUT's resulting state or output after it runs. This is the style `mattpocock-tdd` prescribes.
_Avoid_: black-box testing

**Behaviour verification**:
Asserting on the calls the SUT made to its collaborators. It couples the test to the implementation, so use it only at a true external seam.
_Avoid_: interaction testing (fine, but pick one), call assertions

### Test scope and size

Source: Software Engineering at Google, ch. 11, https://abseil.io/resources/swe-book/html/ch11.html; narrow vs broad integration: https://martinfowler.com/bliki/IntegrationTest.html

**Test scope**:
How much code a test verifies: narrow (unit), medium (integration) or large (end-to-end). It is about the code validated, not the code merely executed.
_Avoid_: test level, test type

**Test size**:
What resources a test may use. Small means one process with no I/O or sleep, medium means one machine with localhost network, large means several machines. Size and scope vary independently.
_Avoid_: test speed, unit vs integration (that is scope)

**Unit test**:
A narrow-scope test of one module's logic through its interface. In the owner's rules it is justified only by a concrete risk (`engineering.md`, Checks and tests).
_Avoid_: small test (that is size)

**Integration test**:
A test that exercises the SUT against real collaborators: database, schema, serialization, a real API.
_Avoid_: component test, functional test, service test, integration test (when doubles replace the collaborators)

**Narrow integration test**:
A test of the SUT's integration code with test doubles in place of the real collaborators. It is not an integration test, so name it in full.
_Avoid_: integration test, component test

**End-to-end test (E2E)**:
A large-scope test through the real UI or API, storage and services, naming every external boundary it replaced.
_Avoid_: system test, broad integration test, functional test, acceptance test

**Hermetic test**:
A test that sets up and tears down everything it needs and assumes nothing about the outside world: no shared database, no test order, no live network.
_Avoid_: isolated test, self-contained test

**Contract test**:
A test that checks a test double or client still matches the real external service's behaviour. Typically run on a schedule, not on every commit.
_Avoid_: API test, schema test, consumer test (unless consumer-driven contracts are meant)

**Production test**:
A test run against the production environment. The owner's rules require explicit permission, dedicated accounts and planned cleanup for it.
_Avoid_: smoke test (a smoke test can run anywhere), live test

**Smoke test**:
A minimal run that shows the system starts and its main path responds at all; it proves availability, not correctness.
_Avoid_: sanity test, health check (that is a runtime probe)

### Oracles and expected values

Sources: characterization test: https://michaelfeathers.silvrback.com/characterization-testing; Go golden-file convention: `src/go/printer/printer_test.go` (`flag.Bool("update", ..., "update golden files")`), https://github.com/golang/go/blob/master/src/go/printer/printer_test.go; owner's definitions: the engineering rules, Checks and tests

**Oracle**:
The independent source that says what the right result is: a spec, a worked example or the previous implementation kept runnable. A test is only as good as its oracle.
_Avoid_: expected value (that is what the oracle yields), ground truth

**Golden test**:
A test that compares output with an independent reference made without the code under test: real anonymized inputs with expected outputs from the canon or the previous behaviour. Owner's term. Go's `-update` "golden files" are snapshot tests under this glossary.
_Avoid_: golden file (when it is regenerated by the code), reference test, baseline test

**Snapshot test**:
A test that prints a structured result in a stable form and compares it with stored text first produced by the implementation. Each later diff is accepted only after reading it.
_Avoid_: expect output, approval test, golden file, characterization test (unless legacy pinning is meant)

**Characterization test**:
A test whose expected value is recorded from what existing code does today, written to pin legacy behaviour before a refactor or rewrite.
_Avoid_: snapshot test (when the code is new), golden master, regression test

**Differential test**:
A test that runs the old and the new implementation on the same inputs and requires equal output. The owner's "keep the old version runnable as the oracle" (`engineering.md`, Refactoring).
_Avoid_: back-to-back test, A/B test, oracle test

**Property-based test**:
A test that generates many inputs and checks an invariant over all of them (round trip, totals balance), shrinking a failure to a minimal case.
_Avoid_: generative test, randomized test, fuzz test

**Fuzz test**:
A test that feeds generated or mutated, often malformed, input to find crashes or invariant breaks. It is coverage-guided where the tool supports it.
_Avoid_: property-based test, random test

**Regression test**:
A test that fails on a specific bug that was fixed and passes after the fix, kept so the bug cannot return. In the owner's cycle a bug fix starts with one.
_Avoid_: reproduction test, bug test, non-regression test

### Test reliability

Sources: flaky: https://abseil.io/resources/swe-book/html/ch11.html and https://testing.googleblog.com/2016/05/flaky-tests-at-google-and-how-we.html; Erratic and Fragile Test: http://xunitpatterns.com/Erratic%20Test.html, http://xunitpatterns.com/Fragile%20Test.html

**Flaky test**:
A test whose verdict changes between runs without any change to the code under test or the test. Meszaros calls it an Erratic Test.
_Avoid_: erratic test, intermittent test, broken test (a broken test fails every time), nondeterministic test

**Nondeterminism**:
The cause, not the symptom: a dependence on time, thread scheduling, ordering, randomness, network or shared state that makes a result vary. A flaky test is the symptom of nondeterminism in the test or in the code.
_Avoid_: flakiness (as a name for the cause), randomness

**Fragile test**:
A test that breaks when code changes in a way that does not change the behaviour it checks. `mattpocock-tdd` calls its usual cause implementation-coupled.
_Avoid_: brittle test, flaky test

**Quarantine**:
Moving a known flaky test out of the blocking set while it is fixed, with an assignee and a tracking issue. It is a temporary state, never a removal.
_Avoid_: skip, disable, ignore

**Retry**:
Rerunning a failed test automatically and taking any pass as a pass. It hides flakiness, so name it explicitly when asking for or forbidding it.
_Avoid_: rerun (a rerun is a human or CI re-execution of a whole job)

### Test adequacy and quality metrics

Sources: CRAP: Savoia, Artima, 2007-07-19, https://www.artima.com/weblogs/viewpost.jsp?thread=210575; mutant states and score: https://stryker-mutator.io/docs/mutation-testing-elements/mutant-states-and-metrics/; equivalent mutants: https://stryker-mutator.io/docs/mutation-testing-elements/equivalent-mutants/; PIT mutators: https://pitest.org/faq/; ub-mode use: https://github.com/unclebob/ub-mode (README, no license; read, not copied)

**Code coverage**:
The share of code (lines or branches) that tests execute. It shows what is unexercised, not what is verified: a test with no assertion still adds coverage.
_Avoid_: test coverage (when the meaning is coverage of requirements), coverage as quality

**Cyclomatic complexity**:
The number of independent paths through a function: one plus its decision points.
_Avoid_: complexity (unqualified), cognitive complexity (a different metric)

**CRAP score**:
Change Risk Anti-Patterns: a per-function risk number that combines cyclomatic complexity with automated-test coverage. ub-mode's `crapper` gate requires each function below 10, a threshold of ub-mode's own.
_Avoid_: crap metric, change risk, complexity score

**Duplication score**:
The structural similarity between two code blocks as a detection tool measures it. ub-mode's `dryer` flags pairs at 0.8 or above. It is a signal for a shared owner (invariant 2 in `engineering.md`), not a mandate to abstract.
_Avoid_: DRY violation, copy-paste rate

**Mutation testing**:
A tool run that generates many small deliberate changes (mutants) to the code and reruns the tests against each, to measure whether the tests notice. Examples: PIT, Stryker, ub-mode's `mutator`.
_Avoid_: mutation check (owner's manual step), fault injection (runtime faults, a different thing)

**Mutant**:
One changed copy of the code that a mutation tool produces, such as `>=` flipped to `>`. The rule that produces it is a mutation operator, called a "mutator" in PIT.
_Avoid_: mutation (for the changed copy), variant

**Killed mutant**:
A mutant that at least one test failed against (a timeout also counts as detected).
_Avoid_: caught mutant, detected (fine in reports, but pick one)

**Survived mutant**:
A mutant that every test passed against: a covered behaviour that no assertion pins.
_Avoid_: surviving mutation, live mutant, escaped mutant

**No-coverage mutant**:
A mutant in code no test executes. It survives by default and points at missing tests, not weak ones.
_Avoid_: survived mutant (keep the two apart)

**Equivalent mutant**:
A mutant whose behaviour is identical to the original, so no test can kill it. Rewrite the code so it cannot occur, or accept a score below 100%.
_Avoid_: false survivor, unkillable mutant

**Mutation score**:
Detected mutants (killed plus timeout) divided by valid mutants (detected plus survived plus no-coverage). Compile and runtime errors are excluded.
_Avoid_: mutation coverage, kill rate

**Mutation check**:
The owner's manual verification step: for each acceptance criterion, break the code or text it checks, by hand or as a small targeted mutation (revert the fix, remove a guard, flip a condition), and see that criterion's check fail. A check that still passes is empty. It is not a mutation-testing run over the repo (`engineering.md`, Self-check).
_Avoid_: mutation test, mutation testing, breaking test

### TDD rhythm

Sources: Martin, "The Cycles of TDD", 2014-12-17, http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html; "make it work, make it right": ub-mode README; attribution to Kent Beck not verified

**Three laws of TDD**:
Martin's line-by-line discipline: write no production code without a failing test, write only enough test to fail, write only enough code to pass it. Martin calls this the nano-cycle.
_Avoid_: TDD rules, strict TDD

**Red-green-refactor**:
Martin's micro-cycle around one complete test: failing test, passing code, cleanup. `mattpocock-tdd` keeps red → green as the loop and moves refactor to review. Use its **vertical slice** for one test plus its implementation, not "micro-cycle".
_Avoid_: micro-cycle, TDD loop

**Test-first**:
Writing tests before the code they test, in any batch size. TDD is its one-test-at-a-time form; the batch form, all tests up front, is what `mattpocock-tdd` calls horizontal slicing and forbids.
_Avoid_: TDD (when tests are written in a batch), test-driven

**Test-after**:
Writing tests once the code exists.
_Avoid_: retrofitted tests, coverage tests

**Make it work, make it right**:
Ordering a change so that a correct, tested result comes first and structural cleanup comes second as its own behaviour-preserving step. ub-mode's two phases; in the owner's cycle the cleanup is the rewrite of development cycle step 3 (`core.md`), not the design-improvement commit, which comes before the behaviour change.
_Avoid_: hack then clean, two-pass
