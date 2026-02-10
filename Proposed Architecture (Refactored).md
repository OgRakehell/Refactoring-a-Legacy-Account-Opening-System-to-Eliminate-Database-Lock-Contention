# Proposed Architecture (Refactored)
### 1. Decouple User Action from Core Processing
When an RM submits an account opening request:

- The system generates a **unique request serial number**

- A single database insert is performed

- The transaction is committed immediately

- RM UI receives a **“Request Accepted”** response

No CBA calls occur at this stage.

This guarantees:

- Minimal lock duration

- Fast UI response

- Durable persistence of intent

### 2. Enforce Idempotency at the Database Layer
Each request serial number is enforced with a **unique constraint.**

Effects:

- Duplicate submissions are safely ignored or acknowledged

- Retries do not create duplicate accounts

- Processing becomes replay-safe

Idempotency is not assumed — it is enforced.

### 3. Introduce a Request Processing Pipeline
A background worker service periodically:

- Selects pending requests in controlled batches

- Processes them in FIFO order where possible

- Pushes account creation requests to CBA

- Updates request status incrementally

Batch sizes are tuned based on:

- CBA throughput tolerance

- Observed latency

- Failure rates

This introduces **intentional backpressure** into the system.

### 4. Explicit State Machine for Requests
Each request moves through defined states, for example:

- ACCEPTED

- VALIDATED

- SENT_TO_CBA

- CBA_SUCCESS

- CBA_FAILED

- RETRY_PENDING

- COMPLETED

This state model provides:

- Full auditability

- Operational visibility

- Deterministic recovery paths

Failures no longer block the system; they are isolated.

### 5. Safe Finalization and Notification
Once CBA confirms account creation:

- Account number is persisted

- Request status transitions to COMPLETED

- RM UI is updated asynchronously

- Customer notifications are triggered automatically

At no point does a user session hold locks or wait on external systems.
