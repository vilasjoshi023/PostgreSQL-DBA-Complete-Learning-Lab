# Daily PostgreSQL DBA Activity Journal

This is the running, topic-wise learning log. Entries are evidence-based and distinguish executed commands from suggested work.

## 2026-11-27 — Topic 10 checkpoint: inspect pg_hba.conf

**Topic:** 10 — Authentication and connectivity  
**Subtopic:** Review active host-based authentication rules  
**Lab:** PostgreSQL 17.11 / CentOS Stream 9 / `postgresql-lab1`

### Command executed

```bash
grep -vE '^[[:space:]]*(#|$)' /var/lib/pgsql/17/data/pg_hba.conf
```

### Observed active rules

```conf
local   all             all                                     peer
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             ::1/128                 scram-sha-256
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```

### Learning outcomes
- `local` matches Unix-domain socket connections.
- `host` matches TCP connections.
- `peer` uses the operating-system user identity for local authentication.
- `scram-sha-256` is password-based authentication for the displayed localhost TCP rules.
- `127.0.0.1/32` is IPv4 loopback; `::1/128` is IPv6 loopback.

### Result and status
**In progress.** HBA rules were inspected. No HBA changes were made. Peer/SCRAM login tests, HBA rule ordering, remote connection, networking and TLS practicals remain pending.

### Next activity
Run and capture:
- `psql -d dba_training` as Linux user postgres, then `SELECT current_user; SELECT current_database();`.
- `psql -h 127.0.0.1 -U dba_user -d dba_training -W`.
- Compare local socket and TCP authentication.

---

## Earlier practicals — Consolidated history (exact dates unavailable)

These are confirmed activities from earlier sessions. Their exact individual dates are not available, so they are not assigned invented daily timestamps.

### Topic 02 — PostgreSQL installation
- Installed PostgreSQL 17.11 on CentOS Stream 9.
- Verified package/version and service unit `postgresql-17`.
- Confirmed service active and enabled during the lab.
- Inspected data and configuration directories, port 5432.
- VM observed at approximately 2 vCPU and 2.7 GiB RAM.

### Topics 01, 03, 04 and 05 — Fundamentals, psql and SQL
- Covered foundational database concepts and an introduction to PostgreSQL architecture.
- Practised psql connections, disconnections and object inspection.
- Created database `dba_training`.
- Created `public.students` with student_id, student_name and age; inserted Rahul, Priya and Amit.
- Added primary key; duplicate key was rejected as expected.
- Practised SELECT, COUNT, WHERE and ORDER BY.
- Created schema `dba_training` and table `employees`; inserted sample rows Vijay/DBA, Arun/Linux and Priya/Developer.
- Practised schema search_path at session and database levels.

### Topic 07 — Database/schema administration
- Inspected database, schema and table ownership.
- Confirmed `public.students` and `dba_training.employees` are different schema-qualified objects.
- Tested search_path persistence after reconnect.
- Tablespace and size-management practicals are not confirmed.

### Topic 08 — Roles and permissions
- Created `dba_user`; granted CONNECT, schema USAGE and table permissions.
- Connected as dba_user and tested SELECT, INSERT and DELETE.
- Revoked write privileges and verified denied DML while SELECT remained available.
- Configured default privileges; tested a new table created after the default grant.
- Created `reporting_user` with read-oriented privileges.
- Created `developer_role` and `developer_user1`; inspected role membership.
- Realistic team-role model was discussed, but execution is not confirmed.

### Topic 09 — PostgreSQL configuration
- Located postgresql.conf, pg_hba.conf, pg_ident.conf and data directory.
- Inspected max_connections, shared_buffers, work_mem, maintenance_work_mem and effective_cache_size.
- ALTER SYSTEM work_mem changed to 8MB, reloaded and reset to 4MB.
- max_connections changed to 150, restart requirement identified and restart performed as Linux root; reset and restarted back to 100.
- Practised session-level work_mem override and RESET.
- Practised database-level work_mem and verified after reconnect.
- Practised role-level work_mem and verified role-over-database priority.
- Demonstrated session > role > database > default precedence for the test setting.
- Removed test role/database work_mem overrides while preserving search_path.

## Daily entry template

Copy this template for each future session:

```markdown
## YYYY-MM-DD — Topic NN: Topic title

**Subtopic:**
**Lab:**

### Concepts learned
-

### Commands executed
```bash
# exact commands
```

### SQL executed
```sql
-- exact SQL
```

### Result / validation
-

### Errors and resolution
-

### Production / safety notes
-

### Status
In progress / Practised / Completed

### Next activity
-
```

Do not store credentials, passwords, private keys or production data. Do not mark suggested commands as executed.
