

## 2026-11-27 — Curriculum review and source-document consolidation

**Scope:** Reviewed the ten newly uploaded DBA/PostgreSQL reference PDFs and aligned them with the existing 26-topic PostgreSQL DBA Master Index.

### Source documents reviewed
- Database Fundamentals & DBA Overview
- GUI & DBA Tools (MySQL & PostgreSQL DBA)
- PostgreSQL Architecture (June 2026)
- PostgreSQL Backup & Recovery
- PostgreSQL Installation & Configuration (June 2026)
- PostgreSQL Performance Tuning
- PostgreSQL Replication
- PostgreSQL Upgrades (two overlapping copies consolidated)
- PostgreSQL User Management & Security (June 2026)

### Outcome
- Consolidated the supplied documents into a sequenced end-to-end learning map.
- Preserved the original 26-topic progress baseline and added explicit coverage for PgBouncer, Linux/network/storage fundamentals, cloud/containers, extension ecosystem, backup tooling, operational excellence and advanced testing.
- Added a safety/correction review for risky or version-sensitive examples in the PDFs.
- Confirmed the current learning lab context is VILASLAB1 / PostgreSQL 18.4; kept the earlier postgresql-lab1 / PostgreSQL 17.11 record separate.
- Current lesson remains Topic 01; departments/employees constraint practical output is pending review.

### Status
Curriculum review documented. No new database lab practical was executed during this session.

### Next activity
Complete the pending Topic 01 constraints/relationships lab, then continue with ACID, normalization and transactions.


## 2026-11-27 — Topic 01 Lesson 1.9: constraints and relationships practical verified

**Environment:** VILASLAB1, PostgreSQL 18.4, database dba_training.

### Practical completed and reviewed
- Queried departments: confirmed 3 rows (DBA, Developer, Testing).
- Queried employees: confirmed 3 rows (Rahul, Priya, Amit).
- Inspected \\d departments: confirmed primary key on department_id, unique constraint on department_name, and referenced-by foreign key fk_department.
- Inspected \\d employees: confirmed primary key on employee_id, unique constraint on email, check constraint salary > 0, and foreign key fk_department to departments.
- Deliberately attempted an employee insert with department_id=99; PostgreSQL correctly rejected it with a foreign-key violation because department 99 does not exist.
- Deliberately attempted a duplicate department ID 10; PostgreSQL correctly rejected it with a primary-key duplicate-key violation.

### Outcome
All expected valid rows and constraint metadata were verified. The two errors were expected negative tests and demonstrate that PostgreSQL is enforcing referential integrity and uniqueness correctly. No corrective action was required.

### Learning status
Topic 01 remains In progress. This constraints/relationships practical is Practised and verified; ACID, normalization and transaction exercises remain.

### Next activity
Lesson 1.10 — ACID properties, normalization and transactions.


## 2026-11-27 — Topic 01 Lesson 1.10: Atomicity practical verified

**Environment:** VILASLAB1, PostgreSQL 18.4, database dba_training.

### Practical completed and reviewed
- Created acid_accounts with account_id primary key, account_name NOT NULL, and balance CHECK (balance >= 0).
- Inserted Account A with 10000.00 and Account B with 5000.00.
- Started a transaction using BEGIN.
- Deducted 1000 from Account A and added 1000 to Account B; both UPDATE commands reported UPDATE 1.
- Queried balances inside the transaction and observed 9000.00 and 6000.00.
- Executed ROLLBACK and queried balances again; original values 10000.00 and 5000.00 were restored.
- A second ROLLBACK produced the expected harmless warning that no transaction was in progress.

### Outcome
Atomicity demonstrated: both changes were rolled back as one unit. No transfer changes remained after rollback.

### Learning status
Atomicity practical is Practised and verified. Topic 01 remains In progress; Consistency, Isolation, Durability, normalization and remaining fundamentals are pending.

### Next activity
Continue ACID with Consistency, then Isolation and Durability.


## 2026-11-27 — Topic 01 Lesson 1.10: Consistency practical verified

**Environment:** VILASLAB1, PostgreSQL 18.4, database dba_training.

### Practical completed and reviewed
- Queried acid_accounts and confirmed Account A = 10000.00 and Account B = 5000.00.
- An attempted CREATE TABLE returned relation already exists; this was harmless because the table had already been created in the Atomicity exercise.
- Attempted to update Account A balance to -500. PostgreSQL rejected the update with check constraint violation for acid_accounts_balance_check.
- Queried balances after the rejected update and confirmed both original balances remained unchanged.
- Inspected the table using \\d acid_accounts and verified CHECK (balance >= 0::numeric), the primary key and NOT NULL account_name.

### Outcome
Consistency demonstrated: PostgreSQL enforced the table's non-negative balance rule and prevented invalid data from being stored. No corrective action was required.

### Learning status
Consistency practical is Practised and verified. Topic 01 remains In progress; Isolation, Durability, normalization and remaining fundamentals are pending.

### Next activity
Continue ACID with Isolation.


## 2026-11-27 — Topic 01 Lesson 1.10: Durability lesson introduced; practical pending

**Environment:** VILASLAB1, PostgreSQL 18.4, database dba_training.

### Concepts covered
- Durability means successfully committed changes should survive a database crash or restart.
- PostgreSQL uses Write-Ahead Logging (WAL) to support crash recovery.
- Under normal synchronous commit settings, PostgreSQL flushes the required WAL records to durable storage before acknowledging commit.
- PostgreSQL can replay WAL during crash recovery; every modified table page does not need to be written before acknowledging each commit.

### Practical status
The proposed lab uses a committed test row in isolation_demo, followed by a controlled PostgreSQL 18 service restart and a query after reconnecting. The user has not yet supplied execution output. Do not mark Durability as practised or verified.

### Other outstanding work
The two-session Isolation lock-wait demonstration has not yet been captured. Earlier attempts showed two backend PIDs, but the pg_stat_activity output did not show a Lock wait; the sessions were observed after their commands had completed.

### Next activity
Complete the Isolation lock-wait test and Durability commit/restart verification, reviewing actual terminal output before updating practical status.


## 2026-11-27 — Topic 01 Lesson 1.10: Isolation lock wait observed; Durability restart practical verified

**Environment:** VILASLAB1, PostgreSQL 18.4, database dba_training.

### Isolation — evidence captured
- Session A (backend PID 11328) began a transaction and updated account 1 by +100 without committing.
- Session B (backend PID 11330) attempted to update the same row by -50.
- From the monitoring query, pg_stat_activity showed PID 11330 as active with wait_event_type = Lock and wait_event = transactionid.
- This confirms PostgreSQL blocked the second transaction while the first transaction held the conflicting row update.
- The user later cancelled a blocked statement and issued BEGIN while a transaction was already active; PostgreSQL correctly warned that a transaction was already in progress. Some later transaction commands were mixed across sessions, so the clean Session A COMMIT → Session B resumes → Session B COMMIT sequence remains to be repeated.
- Do not claim the final balance sequence as a clean isolation proof. The lock-wait observation itself is verified.

### Durability — practical verified
- Inserted and committed row (account_id=2, balance=20000.00) into isolation_demo.
- Confirmed the row before restart.
- Restarted service postgresql-18 from the root shell.
- systemctl status confirmed the service returned to Active: active (running).
- Reconnected to dba_training after restart and queried isolation_demo.
- Confirmed both rows remained, including account_id=2 with balance 20000.00.

**Conclusion:** The committed row survived a normal PostgreSQL service restart. This validates restart persistence, not a simulated crash or power-loss recovery test.

### Operational note
- sudo prompted for a password while logged in as the Linux postgres user and rejected the supplied attempts. The user switched back to root and successfully checked/restarted the service. PostgreSQL database credentials and Linux sudo authorization are separate.

### Learning status
- Isolation lock-wait observation: Practised and verified; clean two-session commit sequence remains.
- Durability restart-persistence practical: Practised and verified.
- Topic 01 remains In progress; normalization, PostgreSQL use cases and architecture overview remain.

### Next activity
Repeat the clean two-session Isolation completion sequence, then continue Topic 01 with normalization and PostgreSQL use cases/architecture overview.
