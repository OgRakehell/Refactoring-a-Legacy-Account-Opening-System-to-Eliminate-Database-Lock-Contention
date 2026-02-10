# Root Cause Analysis

The failure was not due to a single bug but a **systemic architectural flaw**.

## Identified causes:

### 1. Long-lived database transactions

- DB transactions spanned multiple steps, including external API calls to CBA

- Locks were held far longer than necessary

### 2. Synchronous coupling

- RM UI → IIS → DB → CBA was a single blocking chain

- Any slowdown downstream propagated upstream

### 3. Concurrency without control

- No backpressure or throttling mechanism

- Multiple RMs competed for the same DB resources

### 4. Lack of idempotency

- Retries risked duplicate processing

- Failures were difficult to safely reprocess

### 5. Operational opacity

- No durable request tracking

- Failures were hard to audit or replay

The database became the bottleneck and the battlefield.
