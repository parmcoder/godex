# Database

PostgreSQL default: `github.com/jackc/pgx`.

Rules:

- Prefer explicit SQL over hidden query builders.
- Keep SQL close to the repository or query object that owns it.
- Pass `context.Context` to every database call.
- Use no explicit transaction for one atomic SQL statement.
- A repository may own a transaction only for one self-contained repository operation whose atomic boundary cannot be extended by callers.
- The service or use-case layer must own transactions spanning multiple repository operations.
- Never hide `Begin`, `Commit`, or `Rollback` inside a helper when callers may need to add work to the same transaction.
- Repositories participating in a caller-owned transaction must accept the shared `pgx.Tx` or be constructed as transaction-scoped repositories. They must not open nested independent transactions.
- Immediately after a successful `Begin`, use `defer tx.Rollback(ctx)`; commit explicitly once. The deferred rollback is safe after a successful commit.
- Every query in a use case must use the same transaction and context.
- Keep transactions short. Never make slow network calls while holding one open.
- Keep database-specific details out of unrelated domain packages.
- Validate migration and rollback risk before changing schema.
- Map database errors to domain errors at package boundaries, wrapping enough operation and cause context for diagnosis.

## Transaction ownership

| Work | Owner |
| --- | --- |
| Single atomic SQL statement | No explicit transaction |
| Multiple statements in one repository operation | Repository transaction |
| Multiple repositories in one use case | Service-owned transaction |
| Database plus external side effect | Transaction plus compensation or transactional outbox |

PostgreSQL transactions cannot include S3, HTTP APIs, queues, or caches. Make those boundaries explicit:

- Use compensation when a completed step can be safely undone.
- Make retried external operations idempotent.
- Use a transactional outbox when an external event must follow a committed database change reliably.
- Do not call the external system until the database transaction has ended.

## Minimal service-owned pgx transaction

```go
func (s *Service) Transfer(ctx context.Context, from, to int64, amount int64) error {
	tx, err := s.pool.Begin(ctx)
	if err != nil {
		return fmt.Errorf("begin transfer: %w", err)
	}
	defer tx.Rollback(ctx)

	accounts := NewAccountRepository(tx)
	ledger := NewLedgerRepository(tx)

	if err := accounts.Debit(ctx, from, amount); err != nil {
		return fmt.Errorf("debit account %d: %w", from, err)
	}
	if err := accounts.Credit(ctx, to, amount); err != nil {
		return fmt.Errorf("credit account %d: %w", to, err)
	}
	if err := ledger.RecordTransfer(ctx, from, to, amount); err != nil {
		return fmt.Errorf("record transfer: %w", err)
	}
	if err := tx.Commit(ctx); err != nil {
		return fmt.Errorf("commit transfer: %w", err)
	}
	return nil
}
```

`NewAccountRepository` and `NewLedgerRepository` receive the same `pgx.Tx`; neither starts or commits a transaction. Translate known PostgreSQL errors such as constraint violations to domain errors while retaining the wrapped database cause for logs and traces.

Review repositories for:

- connection pool lifecycle and shutdown
- timeout and cancellation behavior
- row closing and scan error handling
- idempotent writes where retries can occur
- tests for no rows, duplicate keys, transaction rollback, and context cancellation
- PostgreSQL-backed integration tests proving commit, rollback, concurrency invariants, and no partial writes
- test data populators for required rows and relations instead of ad hoc setup copied across cases
- setup/teardown that commits known fixture state to the test database and removes it after each test or suite
- stock/inventory changes must test rejected product IDs, unauthorized or missing shop, insufficient stock, successful decrement, failed sale rollback with no sale log, and user isolation
