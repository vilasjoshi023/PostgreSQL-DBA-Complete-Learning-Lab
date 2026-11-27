

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
