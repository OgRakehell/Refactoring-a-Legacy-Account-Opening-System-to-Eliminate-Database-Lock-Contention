# Why This Solves the Original Problem
### Lock contention is eliminated because:
- Database transactions are short-lived

- No external calls occur inside transactions

- Writes are append-based, not blocking

### System stability improves because:
- Load on CBA is throttled and predictable

- Failures are retried safely

- One bad request cannot block others

### Operational control increases because:
- Every request is traceable

- Backlogs are visible

- Processing can be paused or resumed without data loss

## Trade-offs and Considerations
This refactor intentionally accepts:

- Eventual consistency instead of synchronous completion

- Slightly delayed account number issuance

- Additional infrastructure for background processing

These trade-offs are standard in resilient banking systems and were deemed acceptable compared to systemic instability.
