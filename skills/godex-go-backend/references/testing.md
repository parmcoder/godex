# Testing

Default pattern:

- Use TDD for clear small units.
- Use table-driven tests for input/output behavior.
- Use plain `testing` unless a suite adds real value.
- Use suites when the component requires mocks, shared setup, or lifecycle control.
- Use `mockery` for mocks; do not hand-roll large mocks.
- Cover error paths, edge cases, validation, and context cancellation.

Avoid:

- Tests tied to private implementation details.
- Mocking the unit under test.
- Hidden sleeps or timing assumptions.
- Integration tests that require undeclared local services.

Integration tests:

- Use them for pgx, Redis, and Kafka behavior when correctness depends on the real dependency.
- Gate them behind clear build tags or task names if they need local containers.
- Test transaction rollback, cache miss/outage behavior, consumer retry/idempotency, and cancellation.

Verification should start narrow, then broaden when shared packages or contracts changed.
