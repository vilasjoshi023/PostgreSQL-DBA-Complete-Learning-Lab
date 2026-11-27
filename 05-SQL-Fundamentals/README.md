# Topic 05 — SQL Fundamentals

**Status: Partial**

## Objects and data created

### public.students
Columns:
- `student_id INTEGER`
- `student_name VARCHAR(100)`
- `age INTEGER`

Sample records included:
- (1, Rahul, 20)
- (2, Priya, 21)
- (3, Amit, 22)

A primary key was added; a duplicate student_id was rejected as expected.

### dba_training.employees
Columns:
- `employee_id INTEGER PRIMARY KEY`
- `employee_name VARCHAR(100)`
- `department VARCHAR(50)`

Sample records:
- (101, Vijay, DBA)
- (102, Arun, Linux)
- (103, Priya, Developer)

## SQL operations practised

```sql
SELECT * FROM students;
SELECT COUNT(*) FROM students;
SELECT * FROM students WHERE age > 20;
SELECT * FROM students ORDER BY student_name;
```

Also practised CREATE TABLE, INSERT, UPDATE, DELETE and primary-key constraint behaviour.

## Remaining
- Systematic DDL/DML/DQL/DCL/TCL classification.
- ALTER/DROP/TRUNCATE exercises with safe checks.
- GROUP BY, HAVING and aggregate functions.
- NULL handling, expressions and explicit casts.
- Transaction control in Topic 11.
