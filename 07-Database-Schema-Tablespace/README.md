# Topic 07 — Database, Schema and Tablespace Administration

**Status: Partial**

## Practised
- Created database `dba_training`.
- Created schema `dba_training`.
- Created `public.students` and `dba_training.employees`.
- Inspected database, schema and table ownership.
- Compared schema-qualified and unqualified table names.
- Tested session-level search_path.
- Configured database-level search_path and verified it after reconnect.

## Useful commands

```sql
\l
\dn+
\dt *.*
\dp
SHOW search_path;
```

Example:

```sql
SET search_path TO dba_training, public;
ALTER DATABASE dba_training SET search_path TO dba_training, public;
```

## Not yet covered
- Tablespace creation and safe storage placement.
- Database/table/index size reports.
- Object dependencies and decommissioning runbook.
- Provisioning standards and capacity planning.
