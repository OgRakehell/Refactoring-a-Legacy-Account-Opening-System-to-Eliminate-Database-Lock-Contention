# Problem Statement

When multiple RMs attempted to open accounts concurrently:

- Database transactions became blocked by lock waits

- Account opening requests stalled or failed

- Manual refreshes temporarily resolved the issue

- The problem resurfaced predictably under load

Despite repeated operational interventions, the issue persisted for years.
