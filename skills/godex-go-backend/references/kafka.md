# Kafka

Kafka default: `github.com/IBM/sarama`.

Rules:

- Handle consumer group lifecycle carefully.
- Support graceful shutdown from context or signals.
- Make offset commit strategy explicit.
- Prefer idempotent handlers when retries are possible.
- Avoid message loss where possible; document tradeoffs when not.
- Trace and log message processing with topic, partition, offset, and correlation IDs when safe.
- Do not log sensitive message payloads by default.

Review producers for:

- delivery guarantee expectations
- retry and timeout behavior
- partitioning assumptions
- schema/version compatibility

Review consumers for:

- rebalance behavior
- retry and dead-letter strategy
- idempotency
- commit timing
- shutdown behavior
- backpressure
