# Cache

Redis default: `github.com/redis/go-redis`.

Rules:

- Use context-aware calls.
- Set TTLs intentionally. No accidental forever keys.
- Keep cache key patterns centralized and documented.
- Treat cache misses as normal behavior.
- Define safe behavior for Redis outages.
- Avoid scattering serialization details across packages.
- Do not cache secrets or sensitive raw payloads.

Cache design should state:

- key format
- owner package
- TTL
- invalidation path
- miss behavior
- outage behavior
- serialization format

Tests should cover hit, miss, decode failure, outage, cancellation, and TTL intent where practical.
