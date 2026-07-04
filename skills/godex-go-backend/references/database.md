# Database

PostgreSQL default: `github.com/jackc/pgx`.

Rules:

- Prefer explicit SQL over hidden query builders.
- Keep SQL close to the repository or query object that owns it.
- Pass `context.Context` to every database call.
- Make transaction boundaries obvious in names and call flow.
- Do not start transactions in helpers where callers cannot see them.
- Keep database-specific details out of unrelated domain packages.
- Validate migration and rollback risk before changing schema.
- Return domain-friendly errors at package boundaries without losing operational context.

Review repositories for:

- connection pool lifecycle and shutdown
- timeout and cancellation behavior
- row closing and scan error handling
- idempotent writes where retries can occur
- tests for no rows, duplicate keys, transaction rollback, and context cancellation
