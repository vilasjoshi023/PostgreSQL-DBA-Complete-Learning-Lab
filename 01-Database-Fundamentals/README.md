# Topic 01 — Database Fundamentals

**Status: In progress**  
**Current lab:** VILASLAB1, PostgreSQL 18.4, database dba_training

## Syllabus
- Database, DBMS, RDBMS and database server
- Database, instance, schema, table, row, column and data types
- OLTP vs OLAP
- Primary keys, foreign keys, constraints and relationships
- ACID, normalization and transactions
- PostgreSQL use cases and architecture overview

## Confirmed learning so far
- Introduced database, DBMS and RDBMS concepts.
- Worked with databases, schemas, tables, rows and columns.
- Created departments and employees tables in dba_training.
- Inserted and queried three department rows and three employee rows.
- Verified primary-key, unique, not-null, check and foreign-key constraints using \\d.
- Confirmed a foreign-key violation when an employee referenced nonexistent department 99.
- Confirmed a primary-key violation when attempting duplicate department ID 10.
- Both errors were expected negative tests; PostgreSQL behaved correctly.

## Practical schema
- departments.department_id: primary key.
- departments.department_name: NOT NULL and UNIQUE.
- employees.employee_id: primary key.
- employees.employee_name: NOT NULL.
- employees.email: UNIQUE.
- employees.salary: CHECK (salary > 0).
- employees.department_id: foreign key referencing departments.department_id.

## Still to practise
- Clean two-session Isolation completion sequence: Session A COMMIT, blocked Session B resumes, then Session B COMMIT. The lock-wait observation itself has been captured and verified.
- Normalization examples (1NF, 2NF, 3NF).
- SAVEPOINT and additional transaction-control practice.
- OLTP vs OLAP examples and PostgreSQL use cases.
- PostgreSQL architecture overview and practical implications.

## Completion evidence
The constraints/relationships practical has been executed and output reviewed on the current PG18.4 lab. Keep Topic 01 marked in progress until the remaining syllabus, validation checks, troubleshooting exercises and interview review are complete.


## ACID practical — Atomicity

**Status: Practised and verified** on VILASLAB1 / PostgreSQL 18.4 / dba_training.

- Created acid_accounts with a non-negative balance CHECK constraint.
- Inserted two sample accounts with balances 10000.00 and 5000.00.
- Used BEGIN, deducted 1000 from Account A and added 1000 to Account B.
- Verified interim balances of 9000.00 and 6000.00 inside the transaction.
- Executed ROLLBACK and verified that balances returned to 10000.00 and 5000.00.
- The subsequent extra ROLLBACK warning was harmless because no transaction remained active.

**Conclusion:** PostgreSQL rolled back both updates together, demonstrating Atomicity (all or nothing).

Consistency, Isolation and Durability practical status is recorded below. Topic 01 remains In progress.


## ACID practical — Consistency

**Status: Practised and verified** on VILASLAB1 / PostgreSQL 18.4 / dba_training.

- Queried acid_accounts and confirmed balances of 10000.00 and 5000.00.
- Attempted to update Account A to -500; PostgreSQL rejected it due to acid_accounts_balance_check.
- Queried the table again and confirmed original balances remained unchanged.
- Used \\d acid_accounts to verify CHECK (balance >= 0::numeric), primary key and NOT NULL metadata.
- A repeated CREATE TABLE returned relation already exists because the table was already present; no drop/recreate was needed.

**Conclusion:** The CHECK constraint prevented an invalid balance, demonstrating the Consistency property.

Remaining ACID properties: Isolation and Durability. Topic 01 remains In progress.


## ACID practical — Isolation

**Status: Lock-wait observation practised and verified; clean transaction completion sequence still pending** on VILASLAB1 / PostgreSQL 18.4.

- Session A (PID 11328) held an uncommitted update to account 1.
- Session B (PID 11330) attempted to update the same row.
- pg_stat_activity showed PID 11330 as active with wait_event_type = Lock and wait_event = transactionid.
- This confirms a real lock wait caused by the conflicting uncommitted transaction.
- Later attempts included statement cancellation and nested BEGIN warnings; repeat the clean sequence once: commit Session A, allow Session B's update to finish, then commit Session B.

**Conclusion:** PostgreSQL enforces transaction isolation by making a conflicting update wait for the transaction holding the row lock.

## ACID practical — Durability

**Status: Practised and verified** on VILASLAB1 / PostgreSQL 18.4.

- Inserted and committed (account_id=2, balance=20000.00) into isolation_demo.
- Verified the row before restarting the PostgreSQL service.
- Restarted postgresql-18 from the root shell and confirmed systemd reported Active: active (running).
- Reconnected to dba_training and queried isolation_demo; account_id=2 with balance 20000.00 was still present.

**Conclusion:** The committed row survived a normal service restart. This is a restart-persistence test, not a simulated crash or power-loss recovery test. PostgreSQL uses WAL to support crash recovery.

**Remaining ACID follow-up:** Repeat the clean two-session Isolation commit sequence. Topic 01 remains In progress.
