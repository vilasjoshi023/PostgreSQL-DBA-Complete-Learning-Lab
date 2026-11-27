# PostgreSQL DBA Learning Progress

**Curriculum baseline:** PostgreSQL DBA Master Index — 26 topics  
**Supplementary source review:** 10 uploaded PDFs consolidated on 2026-11-27  
**Current active learning lab:** VILASLAB1, PostgreSQL 18.4  
**Earlier lab history:** postgresql-lab1, PostgreSQL 17.11 (kept separate)

## Summary

| Level | Topics | Status snapshot |
|---|---:|---|
| Level 1 — Fundamentals and SQL | 01–06 | Topic 01 in progress; fundamentals and constraints practical verified. Other historical topic evidence remains recorded below. |
| Level 2 — Core administration | 07–12 | Historical hands-on coverage exists for 07–10 in the earlier PG17 lab; Topic 10 connectivity tests were pending in that record. |
| Level 3 — Backup, recovery and performance | 13–17 | Not started in the structured course |
| Level 4 — Advanced and enterprise | 18–26 | Not started in the structured course |

**Important:** Reading a PDF or discussing a topic is not the same as completing a lab. Status is evidence-based.

## Topic tracker

| # | Topic | Status | Evidence / remaining work |
|---:|---|---|---|
| 01 | Database fundamentals | In progress | Covered database/DBMS/RDBMS, database vs server vs instance, schema/table/row/column/types, OLTP/OLAP, primary/foreign keys, constraints and relationships. On current VILASLAB1 PG18.4, created departments and employees, inserted 3 rows into each, verified PK/UNIQUE/NOT NULL/CHECK/FK metadata using \\d, and confirmed expected rejection of a nonexistent department FK and duplicate department PK. Atomicity transaction practical verified: created acid_accounts, performed two updates inside BEGIN, observed interim balances, and ROLLBACK restored original balances. Remaining: Consistency, Isolation, Durability, normalization, and PostgreSQL use cases/architecture overview. |
| 02 | PostgreSQL installation and prerequisites | Historical Practised; current PG18 lab verify | PostgreSQL 17.11 installation was previously practised on CentOS Stream 9. Current VILASLAB1 PG18.4 service/version/path are known from the active learning thread. Revisit installation runbook, dependency handling, sizing, SELinux/firewall and rollback safely. |
| 03 | PostgreSQL architecture | Partial | Basic architecture introduction and source reading. Deep process lifecycle, memory, WAL, MVCC, background workers, storage and query execution labs remain. |
| 04 | psql and pgAdmin | Partial | psql connections, meta-commands and object inspection practised. pgAdmin server registration/query tool/monitoring lab remains unverified. |
| 05 | SQL fundamentals | Partial | Basic table creation, inserts, selects, filters, sorting and aggregates have historical practice. Full SQL categories, NULL, GROUP BY/HAVING, joins and transaction labs remain. |
| 06 | Advanced SQL and objects | Not started | Joins, subqueries, CTEs, recursive CTEs, window functions, views/materialized views, sequences/identity, functions/procedures/triggers, extensions, JSON/JSONB and arrays. |
| 07 | Database/schema/tablespace administration | Historical Partial | Database/schema/table creation and search_path/ownership inspection practised in earlier lab. Tablespaces, dependencies, sizing, provisioning/decommissioning remain. |
| 08 | Roles and privileges | Historical Practised | Earlier PG17 lab included role creation, membership, GRANT/REVOKE, default privileges and access tests. Repeat/verify in PG18 as needed; complete ownership and safe role cleanup. |
| 09 | Configuration management | Historical Practised | Earlier PG17 lab included config inspection, SHOW/ALTER SYSTEM, reload/restart, parameter precedence and rollback. Revalidate version-specific behaviour on PG18. |
| 10 | Authentication and connectivity | Historical In progress | Earlier PG17 HBA rules were inspected; peer/SCRAM login tests, first-match behaviour, remote access, firewall/DNS/routing, TLS and app connectivity remained. |
| 11 | Transactions and concurrency | Not started | ACID, BEGIN/COMMIT/ROLLBACK/savepoints, MVCC, isolation, locks, deadlocks, long transactions and safe remediation. |
| 12 | Storage and maintenance | Not started | Heap/pages/TOAST, indexes/bloat, VACUUM/ANALYZE/VACUUM FULL, autovacuum, statistics, wraparound and growth. |
| 13 | Backup and restore | Not started | pg_dump/pg_restore/pg_dumpall, pg_basebackup, logical/physical strategy, object-level restore, validation and restore drills. |
| 14 | WAL and PITR | Not started | WAL, checkpoints, archiving, base backups, PITR, RPO/RTO and archive troubleshooting. |
| 15 | Indexing and query optimization | Not started | Index types/design, EXPLAIN/ANALYZE, scans, joins, planner statistics and query tuning. |
| 16 | Performance diagnosis and tuning | Not started | pg_stat views, pg_stat_statements, CPU/memory/I/O, memory/connections/WAL/autovacuum/checkpoints and pooling. |
| 17 | Monitoring and alerting | Not started | Logs, health checks, Prometheus/exporter/Grafana, pgBadger, alerting and capacity planning. |
| 18 | Streaming replication | Not started | Physical replication, sync/async, slots, WAL retention, lag and standby recovery. |
| 19 | Logical replication | Not started | Publisher/subscriber, publications/subscriptions, initial sync, schema limitations and migration. |
| 20 | High availability and failover | Not started | Switchover/failover, fencing, split-brain prevention, Patroni, consensus, HAProxy, rejoin and failback. |
| 21 | Security and auditing | Not started | Least privilege, TLS/certificates, RLS, pgaudit, secret rotation, encryption and compliance. |
| 22 | Partitioning and large data design | Not started | Range/list/hash, pruning, indexes, retention, attach/detach and partition maintenance. |
| 23 | Upgrades, migration and capacity planning | Not started | Minor/major upgrades, pg_upgrade, logical migration, extensions, validation, rollback and cutover. |
| 24 | Production troubleshooting and incident response | Not started | Service, connection, query, lock, disk/WAL, archive, replication and recovery incidents; RCA. |
| 25 | Automation and DBA scripting | Not started | Bash/SQL/Python checks, backup automation, cron/systemd timers, alerts, idempotency and error handling. |
| 26 | Final PostgreSQL DBA project | Not started | Integrated build, permissions, realistic workload, tuning, backup/recovery, replication/failover, monitoring, incident simulations and mock interview. |

## Expanded coverage added from source review

The consolidated learning map adds explicit modules for:
- PgBouncer and connection-pooling operations.
- Replication-slot lifecycle and WAL-retention safeguards.
- Cloud-managed PostgreSQL, Docker and Kubernetes/operator awareness.
- PostgreSQL extension ecosystem, FDW, pgBackRest, Barman, pg_repack, pgBadger and pgaudit.
- Linux/network/storage DBA foundations, operational runbooks, SLI/SLO and incident management.

See [CURRICULUM-REVIEW-AND-EXPANSION.md](CURRICULUM-REVIEW-AND-EXPANSION.md) for the full syllabus and source-document safety review.

## Historical evidence from earlier PG17 lab

- Created database/schema/tables and inspected object ownership/search_path.
- Practised basic SQL and primary-key enforcement.
- Created users/roles and tested table privileges.
- Practised default privileges and role membership.
- Inspected PostgreSQL configuration files and parameter precedence.
- Changed/reverted selected test parameters, including a restart-required setting.
- Inspected pg_hba.conf rules; connection tests remained pending.

Do not assume these commands were run on the current VILASLAB1 PG18.4 environment.

## Current next action

Continue Topic 01 with the remaining ACID properties (Consistency, Isolation, Durability), normalization and PostgreSQL use cases/architecture overview. Atomicity rollback practical is verified.

## Completion standard

A topic can be marked **Practised** only after commands are executed and outputs reviewed. Mark **Completed** only when all listed subtopics, validation checks, troubleshooting exercises and interview review are complete.
