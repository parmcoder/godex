# Code Review

Review for production behavior before style.

Check:

- Package boundaries match domain ownership.
- Public APIs are intentional and stable.
- Interfaces are justified and near consumers.
- Errors preserve useful context without exposing secrets.
- All external I/O accepts `context.Context`.
- Config is validated and has safe defaults where appropriate.
- Logs use `log/slog`, include useful IDs, and avoid sensitive data.
- Tests cover normal behavior, edge cases, errors, and cancellation.
- Database transactions and Kafka commits have clear boundaries.
- Swagger docs, mocks, and Wire providers can be regenerated.
- Health, readiness, metrics, and graceful shutdown fit Kubernetes.

Call out over-engineering directly. A smaller standard-library change is better than a framework when it solves the problem.
