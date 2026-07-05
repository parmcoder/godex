# Checklists

## Code Review

- Package boundaries are domain-driven.
- Dependencies follow project convention or Godex defaults.
- Interfaces are justified and near consumers.
- Errors are clear and safe.
- Tests cover behavior, errors, and cancellation.
- Generated docs, mocks, and providers are reproducible.

## Testing

- TDD used for clear small units.
- Table tests used where they make cases clearer.
- Suites used only when shared setup or mocks help.
- Mockery mocks are regenerated through a task.
- CI unit/service tests run without real PostgreSQL, Redis, Kafka, S3, or external APIs.
- Local integration tests document required containers and commands, and stay out of default CI unless a dedicated integration job exists.
- Integration tests use setup/teardown plus small data populators for database rows, cache keys, and messages.
- Repository transaction/invariant changes include real DB integration coverage or explicitly report the gap.

## API Readiness

- `net/http` first; `gin` only when justified.
- `/healthz`, `/readyz`, `/metricz` exist for services.
- Swagger docstrings cover handlers and models.
- Error responses are consistent.

## Database Readiness

- pgx calls accept context.
- SQL is explicit.
- Transactions have clear boundaries.
- Migration and rollback risk is reviewed.
- Repository invariants are covered against real PostgreSQL when SQL behavior matters.
- Test fixtures are committed to the test database before assertions and cleaned up afterward.

## Kafka Readiness

- Consumer lifecycle is explicit.
- Shutdown is graceful.
- Offset commit strategy is documented.
- Handlers are idempotent where retries can happen.

## Observability Readiness

- `log/slog` used for structured logs.
- OTel spans cover important operations.
- Jaeger works locally or is documented.
- Secrets and sensitive payloads are never logged.

## Kubernetes Readiness

- Liveness is cheap.
- Readiness reflects serving ability.
- Metrics are stable.
- Shutdown respects termination windows.
