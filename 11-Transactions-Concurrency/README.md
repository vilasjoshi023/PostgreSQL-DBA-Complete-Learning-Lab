# Topic 11 — Transactions and Concurrency

**Status: Not started**

## Syllabus
- BEGIN, COMMIT, ROLLBACK and savepoints.
- MVCC and transaction IDs (XIDs).
- Transaction isolation levels.
- Locks, blocking sessions and deadlocks.
- Long-running and idle-in-transaction sessions.
- Safe investigation and remediation.

## Planned lab outcomes
- Demonstrate commit and rollback using lab tables.
- Create two concurrent sessions and observe blocking.
- Inspect locks and blocked queries.
- Reproduce a controlled deadlock in a disposable lab.
- Learn safe termination decisions and transaction-risk assessment.

## Initial inspection queries

```sql
SELECT pid, usename, state, xact_start, query
FROM pg_stat_activity
WHERE xact_start IS NOT NULL
ORDER BY xact_start;
```

No practical has been recorded yet.
