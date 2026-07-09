# Testing

Default pattern:

- Use TDD for clear small units.
- Use table-driven tests for input/output behavior.
- Use plain `testing` unless a suite adds real value.
- Use suites when the component requires mocks, shared setup, or lifecycle control.
- Use `mockery` for mocks; do not hand-roll large mocks.
- Cover error paths, edge cases, validation, and context cancellation.

Test lanes:

- Unit/service tests are CI-friendly by default: no real PostgreSQL, Redis, Kafka, S3, or external APIs.
- Use existing boundary mocks such as `httpmock`, `pgxmock`, `redismock`, Sarama mocks, generated mockery mocks, or tiny stdlib fakes.
- Unit/service tests protect service contracts, error mapping, retries, validation, cancellation, and orchestration.
- Integration tests are local-only by default when they require real PostgreSQL, Redis, Kafka, or HTTP/API calls.
- Gate local integration tests behind clear build tags or task names, and document the required containers and command.
- Integration suites should provide small test data populators for PostgreSQL rows, cache entries, and Kafka messages so setup is fast, explicit, and reusable.

Avoid:

- Tests tied to private implementation details.
- Mocking the unit under test.
- Hidden sleeps or timing assumptions.
- Integration tests that require undeclared local services.
- Hand-written fake DB/cache/Kafka layers when the project already has `pgxmock`, `redismock`, Sarama mocks, or test containers.

Integration tests:

- Use them for pgx, Redis, and Kafka behavior when correctness depends on the real dependency.
- Gate them behind clear build tags or task names if they need local containers.
- Test transaction commit, rollback, concurrency invariants, no partial writes, cache miss/outage behavior, consumer retry/idempotency, and cancellation.
- Do not mock the repository under test when verifying PostgreSQL transaction behavior or data invariants.
- PostgreSQL tests prove commit, rollback, concurrency invariants, no partial writes, ownership isolation, not-found mapping, and relevant domain invariants against real SQL and schema assumptions.
- Redis tests cover real get/set, miss behavior, TTL, serialization, and outage behavior where relevant.
- Kafka tests cover publish/consume, topic assumptions, idempotency, retry, offset/ack behavior, and cancellation.
- HTTP/API tests cover real route wiring, middleware, auth boundaries, request/response contracts, and generated docs compatibility where applicable.
- Database and cache tests must use setup/teardown that creates known state, commits it to the test database or test cache, and cleans it afterward.
- Verify persisted effects from the real dependency: query PostgreSQL after commit, read Redis after set/expire, and consume Kafka messages after publish.

Verification should start narrow, then broaden when shared packages or contracts changed.
