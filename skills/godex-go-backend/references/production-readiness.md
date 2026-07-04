# Production Readiness

Check:

- Graceful shutdown handles HTTP server, database pool, Redis client, Kafka consumers/producers, traces, and metrics.
- `/healthz` checks process liveness only.
- `/readyz` reflects required dependencies and startup state.
- `/metricz` exposes metrics or metrics-related health information consistently.
- Config validates before starting listeners or workers.
- Logs and spans avoid sensitive data.
- Migrations have rollback and deployment risk reviewed.
- Timeouts, retries, and cancellation are explicit.
- Background workers stop on context cancellation.
- API docs can be rebuilt for frontend consumers.
- Operational dashboards or alerts can use stable health and metrics surfaces.

Do not mark a service production-ready just because tests pass. Readiness includes runtime behavior, failure modes, and operator usability.
