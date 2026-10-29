# Reliability: monitoring, overload, data correctness, reconciliation

How systems fail in production and how good ones stay correct. Read it when you design or review a worker, a queue, a schema or transaction, a retry, a config rollout, an alert or a reconcile loop.

Entry format and precedence: [SKILL.md](SKILL.md).

## Google SRE book

- **Measure the four golden signals.** Latency, traffic, errors and saturation of the user-facing path. Supports: core.md › Development cycle, step 2 (failure and how it is noticed). [golden signals][sre-gs]
- **Alert on symptoms, not causes; every page is actionable.** The symptom says what is broken; the cause says why. Supports: core.md › Development cycle, step 2 (how it is noticed). [symptoms vs causes][sre-sym]
- **Bound retries.** At most a few attempts per request, a budget per client, randomised exponential backoff; clients throttle themselves when the backend rejects. Supports: no owner rule; advisory. [deciding to retry][sre-retry], [client throttling][sre-thr]
- **Propagate deadlines.** Pass the caller's remaining time down; check it before each expensive stage. Supports: no owner rule; advisory. [deadlines][sre-dl]
- **Degrade before you fall over.** Shed load or serve cheaper results instead of failing everything. Supports: no owner rule; advisory. [load shedding][sre-shed]

## PostgreSQL correctness: Brandur Leach and the PostgreSQL 17 docs

- **A foreign mutation cannot be rolled back.** Group local writes into atomic phases between foreign calls; store a recovery point per phase under an idempotency key, so a retry resumes. Supports: no owner rule; advisory. [idempotency keys][br-idem]
- **Never enqueue into another system inside a transaction.** A worker can start before the commit. Stage the job in a table in the same transaction; a drain sends it after commit. Supports: no owner rule; advisory. [job drain][br-drain]
- **Know what Read Committed allows.** One statement can see an inconsistent snapshot; it suits simple row updates, not complex search conditions. Repeatable Read and Serializable callers must retry on serialisation failure. Supports: no owner rule; advisory. [isolation][pg-iso]
- **Take locks in a consistent order.** That prevents deadlocks. Supports: no owner rule; advisory. [deadlocks][pg-dl]
- **Use `SKIP LOCKED` only for queue-like tables.** It returns an inconsistent view by design. Supports: no owner rule; advisory. [locking clause][pg-skip]

## Cloudflare: postmortems and workerd

- **Treat generated config like user input.** On 2025-11-18 a generated feature file doubled, passed a hard limit of 200 (about 60 in use) and crashed the proxy through an `unwrap` on an error. Fixes: validate generated files, add global kill switches, keep error reports from exhausting resources. Supports: core.md › Engineering (check a fact at its boundary; generated config crosses one). [2025-11-18][cf25]
- **Roll out in stages; bound the cost of every rule.** On 2019-07-02 one backtracking regex used all CPU after a global, unstaged rule push. Fixes: a regex engine with run-time guarantees, profiling rules in tests, staged rollout. Supports: no owner rule; advisory. [2019-07-02][cf19]
- **Pass capabilities, not global names; never break old code.** workerd wires services through explicit bindings, and its version is a compatibility date. Supports: engineering.md › Design (reach another module only through its public contract). [workerd README][wd]

## Kubernetes: API conventions and the controller pattern

- **Be level-based, not edge-based.** Act on the current gap between desired and observed state, so a missed event does no harm. Supports: no owner rule in engineering.md or core.md; advisory. [conventions][k-level], [controllers][k-ctrl]
- **Keep `spec` (desired) apart from `status` (observed).** Report higher-level status through conditions. Supports: engineering.md › Invariants 2 (one owner per piece of knowledge). [spec and status][k-spec]
- **Use optimistic concurrency.** A write carries the version it read and fails if the object changed. Supports: no owner rule; advisory. [concurrency control][k-cc]
- **Shape a controller as a key queue and an idempotent sync.** Enqueue keys; a worker fetches the current object by key, converges actual to desired, updates status and requeues with rate limiting on error. Supports: no owner rule; advisory. [processNextWorkItem][k-pnw], [syncHandler][k-sync]

[sre-gs]: https://sre.google/sre-book/monitoring-distributed-systems/#xref_monitoring_golden-signals
[sre-sym]: https://sre.google/sre-book/monitoring-distributed-systems/#symptoms-versus-causes-g0sEi4
[sre-retry]: https://sre.google/sre-book/handling-overload/#deciding-to-retry-4ksZczHj
[sre-thr]: https://sre.google/sre-book/handling-overload/#client-side-throttling-a7sYUg
[sre-dl]: https://sre.google/sre-book/addressing-cascading-failures/#xref_cascading-failure_latency-and-deadlines
[sre-shed]: https://sre.google/sre-book/addressing-cascading-failures/#xref_cascading-failure_load-shed-graceful-degredation
[br-idem]: https://brandur.org/idempotency-keys#atomic-phases
[br-drain]: https://brandur.org/job-drain
[pg-iso]: https://www.postgresql.org/docs/17/transaction-iso.html#XACT-READ-COMMITTED
[pg-dl]: https://www.postgresql.org/docs/17/explicit-locking.html#LOCKING-DEADLOCKS
[pg-skip]: https://www.postgresql.org/docs/17/sql-select.html#SQL-FOR-UPDATE-SHARE
[cf25]: https://blog.cloudflare.com/18-november-2025-outage/
[cf19]: https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/
[wd]: https://github.com/cloudflare/workerd/blob/1568dcf/README.md#L26-L28
[k-level]: https://github.com/kubernetes/community/blob/440e496/contributors/devel/sig-architecture/api-conventions.md#L312
[k-ctrl]: https://github.com/kubernetes/website/blob/77904cb/content/en/docs/concepts/architecture/controller.md#L108
[k-spec]: https://github.com/kubernetes/community/blob/440e496/contributors/devel/sig-architecture/api-conventions.md#L280-L300
[k-cc]: https://github.com/kubernetes/community/blob/440e496/contributors/devel/sig-architecture/api-conventions.md#L1146
[k-pnw]: https://github.com/kubernetes/sample-controller/blob/v0.37.1/controller.go#L200-L236
[k-sync]: https://github.com/kubernetes/sample-controller/blob/v0.37.1/controller.go#L238-L241
