# PostgreSQL DBA Learning Progress

**Curriculum:** PostgreSQL DBA Master Index — 26 topics  
**Lab:** CentOS Stream 9, PostgreSQL 17.11, hostname `postgresql-lab1`  
**Progress snapshot:** 2026-11-27

## Summary

| Level | Topics | Current position |
|---|---:|---|
| Level 1 — Fundamentals and SQL | 01–06 | 01–05 partial/practised; 06 not started |
| Level 2 — Core administration | 07–12 | 07 partial; 08–09 practised; 10 in progress; 11–12 not started |
| Level 3 — Backup, recovery and performance | 13–17 | Not started |
| Level 4 — Advanced and enterprise | 18–26 | Not started |

**Topics reached:** 10 of 26 (38.5%). This is a topic-reach indicator, not a claim that 38.5% of all syllabus subtopics are mastered.

## Topic tracker

| # | Topic | Status | Confirmed coverage / remaining work |
|---:|---|---|---|
| 01 | Database fundamentals | Partial | Basic database/DBMS/RDBMS, database/schema/table/row/column, primary key, simple constraints and PostgreSQL introduction. Deeper OLTP/OLAP, ACID, normalization, relationships and architecture overview need review/practice. |
| 02 | PostgreSQL installation and prerequisites | Practised | Installed PostgreSQL 17.11 on CentOS Stream 9; package/version checks, initialization/service checks, service enablement, data/config locations and basic validation. Revisit detailed resource/filesystem planning and install troubleshooting as a formal runbook. |
| 03 | PostgreSQL architecture | Partial | Basic client/server and architecture introduction. Postmaster/backend detail, shared memory, background workers, WAL/checkpoints, memory internals and data directory/storage internals remain. |
| 04 | psql and pgAdmin | Partial | psql connection/disconnection, database/schema/table/object inspection, meta-commands and SHOW. pgAdmin installation/registration/query-tool practical is not confirmed. |
| 05 | SQL fundamentals | Partial | Created tables/rows; practised CREATE, INSERT, SELECT, UPDATE, DELETE, primary key, WHERE, ORDER BY and COUNT. Broader DDL/DML/DQL/DCL/TCL, grouping, aggregates, NULL handling, casts and transactions remain. |
| 06 | Advanced SQL and database objects | Not started | Joins, subqueries, CTEs, recursive CTEs, window functions, views/materialized views, sequences/identity, functions/procedures/triggers, extensions, JSON/JSONB and arrays. |
| 07 | Database, schema and tablespace administration | Partial | Created database `dba_training`, schema `dba_training`, tables; explored ownership and search_path. Tablespaces, dependencies, database/table/index sizing, provisioning and decommissioning remain. |
| 08 | Users, roles and privileges | Practised | Created login/group roles; GRANT/REVOKE; CONNECT/USAGE/table permissions; separate-user login and DML validation; default privileges; role membership; read-oriented reporting role; developer role model. Production team-role design and sequence/function privilege coverage need more validation. |
| 09 | PostgreSQL configuration | Practised | Inspected postgresql.conf, pg_hba.conf, pg_ident.conf; SHOW, ALTER SYSTEM, pg_settings, pg_file_settings; reload vs restart; work_mem session/database/role settings; max_connections restart and rollback; precedence and reset. |
| 10 | Authentication and connectivity | In progress | Inspected live HBA rules: local socket uses peer; localhost IPv4/IPv6 TCP uses scram-sha-256; replication entries inspected. Peer/SCRAM tests, HBA first-match behaviour, host/hostssl/reject, remote connectivity, firewall/DNS/routing, TLS and app connectivity remain. |
| 11 | Transactions and concurrency | Not started | BEGIN/COMMIT/ROLLBACK/savepoints, MVCC/XIDs, isolation levels, locks/blocking/deadlocks and long transactions. |
| 12 | Storage and maintenance | Not started | Heap/pages/tuples/TOAST, indexes/bloat, VACUUM/ANALYZE/VACUUM FULL, autovacuum, statistics, wraparound and storage growth. |
| 13 | PostgreSQL backup and restore | Not started | Logical/physical backups, pg_dump/pg_restore/pg_dumpall, pg_basebackup, restore scopes, validation, retention and restore drills. |
| 14 | WAL and point-in-time recovery | Not started | WAL/checkpoints/archiving, archive_mode/archive_command, base backups, PITR, RPO/RTO and archive troubleshooting. |
| 15 | Indexing and query optimization | Not started | Index types/design, selectivity, scans, EXPLAIN/ANALYZE, planner estimates and SQL/index tuning. |
| 16 | PostgreSQL performance tuning | Not started | pg_stat views, pg_stat_statements, CPU/memory/I/O, tuning parameters, checkpoints, WAL, autovacuum, pooling and baselines. |
| 17 | Monitoring and alerting | Not started | Logs, health checks, statistics, Prometheus/exporter/Grafana, alerting and capacity planning. |
| 18 | Streaming replication | Not started | Primary/standby, physical replication, sync/async, slots, WAL retention, lag and standby recovery. |
| 19 | Logical replication | Not started | Publications/subscriptions, initial sync, monitoring, schema limitations and migration use cases. |
| 20 | High availability and failover | Not started | Switchover/failover, promotion, split-brain/fencing, Patroni, consensus, HAProxy, rejoin and consistency. |
| 21 | Security and auditing | Not started | Least privilege, TLS/certs, secret rotation, audit logging/pgaudit, encryption and compliance reviews. |
| 22 | Partitioning and advanced database design | Not started | Range/list/hash partitioning, pruning, maintenance/retention, partition indexes and large-table design. |
| 23 | Upgrades, migration and capacity planning | Not started | Minor/major upgrades, pg_upgrade/logical migration, extension compatibility, rollback, capacity and cutover. |
| 24 | Production troubleshooting and incident response | Not started | Service failures, connection exhaustion, slow queries, locks, disk/WAL/archive issues, replication/recovery incidents and RCA. |
| 25 | Automation and DBA scripting | Not started | Bash/SQL checks, cron/systemd timers, backup automation, monitoring, logging, error handling and idempotency. |
| 26 | Final PostgreSQL DBA project | Not started | End-to-end build, permissions, realistic workload, backup/recovery, replication/failover, dashboards, incident simulations and mock interview. |

## Confirmed practical evidence

### Topic 07 — Database/schema
- Created `dba_training` database and `dba_training` schema.
- Created `public.students` and `dba_training.employees`.
- Inspected ownership and schema search_path.
- Configured database-level search_path and verified after reconnect.
- Tablespace and size-management practicals not confirmed.

### Topic 08 — Roles/privileges
- Created and tested `dba_user`.
- Created `reporting_user` with read-oriented grants.
- Created `developer_role` and `developer_user1`, verified membership.
- Granted/revoked table permissions and tested allowed/denied DML.
- Configured default privileges and tested a subsequently created table.
- Proposed team roles `dba_team`, `developer_team`, `testing_team` are not confirmed as executed.

### Topic 09 — Configuration
- Inspected configuration files and settings.
- Changed work_mem using ALTER SYSTEM, reloaded, reset and reloaded.
- Changed max_connections to 150, restarted as Linux root, verified, reset and restarted back to 100.
- Practised session/database/role work_mem settings and precedence; removed test role/database overrides.
- Observed values after cleanup: max_connections=100, shared_buffers=128MB, work_mem=4MB, maintenance_work_mem=64MB, effective_cache_size=4GB. Revalidate before production use; effective_cache_size is a planner estimate, not reserved memory.

### Topic 10 — Authentication
Current non-comment HBA rules observed:

```conf
local   all             all                                     peer
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             ::1/128                 scram-sha-256
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```

The learner ran:

```bash
grep -vE '^[[:space:]]*(#|$)' /var/lib/pgsql/17/data/pg_hba.conf
```

The output confirms these configured rules. The actual peer and password login tests are still pending.

## Interview preparation

| Track | Status |
|---|---|
| Fundamentals/architecture | Basic coverage; structured revision needed |
| SQL | Basic exercises; advanced SQL pending |
| Administration/roles/configuration | Hands-on coverage |
| Backup and recovery | Not started |
| Performance/indexing | Not started |
| Replication and HA | Not started |
| Production support/RCA | Not started |
| Senior DBA scenarios | Not started |

## Next action

Continue Topic 10:
1. Test peer over Unix socket as Linux `postgres`.
2. Test SCRAM over TCP using `127.0.0.1` and a lab login.
3. Compare socket vs TCP.
4. Learn HBA rule order before making any edits.
