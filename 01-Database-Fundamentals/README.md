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
