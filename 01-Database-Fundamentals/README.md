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
- ACID properties with a transaction example.
- Normalization examples (1NF, 2NF, 3NF).
- BEGIN, COMMIT, ROLLBACK and SAVEPOINT.
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

Remaining ACID properties: Consistency, Isolation and Durability. Topic 01 remains In progress.


## ACID practical — Consistency

**Status: Practised and verified** on VILASLAB1 / PostgreSQL 18.4 / dba_training.

- Queried acid_accounts and confirmed balances of 10000.00 and 5000.00.
- Attempted to update Account A to -500; PostgreSQL rejected it due to acid_accounts_balance_check.
- Queried the table again and confirmed original balances remained unchanged.
- Used \\d acid_accounts to verify CHECK (balance >= 0::numeric), primary key and NOT NULL metadata.
- A repeated CREATE TABLE returned relation already exists because the table was already present; no drop/recreate was needed.

**Conclusion:** The CHECK constraint prevented an invalid balance, demonstrating the Consistency property.

Remaining ACID properties: Isolation and Durability. Topic 01 remains In progress.


## ACID practical — Durability lesson

**Concepts introduced; practical not yet verified** on VILASLAB1 / PostgreSQL 18.4.

- Durability means committed changes should survive a database crash or restart.
- PostgreSQL uses Write-Ahead Logging (WAL) to support crash recovery.
- Under normal synchronous commit settings, required WAL records are flushed to durable storage before a successful commit is acknowledged.
- During crash recovery, PostgreSQL replays WAL as needed.

**Pending lab:** Insert and commit a test row in isolation_demo, verify it, perform a controlled restart of the PostgreSQL 18 service, reconnect and verify the committed row remains. Awaiting actual user execution output; not marked practised.

**Isolation status:** The two-session lock-wait practical is still pending; backend PIDs were identified, but the monitoring output did not capture a Lock wait.
