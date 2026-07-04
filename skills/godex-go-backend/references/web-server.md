# Web Server

Default to `net/http`. Use `gin` only when routing groups, middleware ecosystem, or established project convention justifies it.

Required endpoints:

- `/healthz`: basic process liveness. Avoid dependency checks.
- `/readyz`: readiness checks for required dependencies and startup state.
- `/metricz`: metrics endpoint or metrics-related health information. If the project already exposes Prometheus elsewhere, route consistently.

Kubernetes behavior:

- Keep `/healthz` cheap and reliable.
- Make `/readyz` fail when the service should stop receiving traffic.
- Use clear status codes and short response bodies.
- Do not leak internal dependency details to public clients unless the endpoint is private.

Handlers:

- Accept `context.Context` through request context.
- Decode and validate input at the boundary.
- Return consistent error shapes.
- Add Swagger docstrings for handlers and request/response models when the API is documented.
- Keep handler logic thin; move domain behavior into testable packages.

Logging:

- Use `log/slog`.
- Log request IDs or trace IDs when available.
- Log enough to debug operations and audit important transitions.
- Avoid noisy per-loop or success logs unless they serve operations.
