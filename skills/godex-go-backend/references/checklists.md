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
- Integration tests document required dependencies.

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
