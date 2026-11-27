# Curriculum Review and Expansion — Source PDFs + DBA Master Index

**Review date:** 2026-11-27  
**Primary curriculum:** PostgreSQL DBA Master Index (26 topics)  
**Supporting material reviewed:** the ten PDFs listed below.  
**Policy:** preserve the 26-topic learning sequence; add missing material as subtopics and dedicated lab tracks rather than silently skipping or replacing topics.

## 1. Source documents reviewed

1. Database Fundamentals & DBA Overview.pdf
2. GUI & DBA Tools (MySQL & PostgreSQL DBA).pdf
3. PostgreSQL Architecture_Jun2026(1).pdf
4. PostgreSQL Backup & Recovery.pdf
5. PostgreSQL Installation & Configuration_june2026.pdf
6. PostgreSQL Performance Tuning.pdf
7. PostgreSQL Replication.pdf
8. PostgreSQL Upgrades.pdf
9. PostgreSQL Upgrades_june2026.pdf
10. PostgreSQL User Management & Security - Jun2026.pdf

The two PostgreSQL upgrade PDFs substantially overlap. Treat them as one upgrade module and use the June 2026 copy as a supplementary/duplicate reference, not as a separate topic.

## 2. Consolidated end-to-end curriculum

### Level 1 — Database, SQL and PostgreSQL foundations

| Topic | Required coverage | Source alignment |
|---|---|---|
| 01. Database fundamentals and DBA role | Database/DBMS/RDBMS/ORDBMS; database vs server vs instance/cluster; schemas, tables, rows, columns, data types; keys, constraints and relationships; OLTP/OLAP; ACID; normalization (1NF–3NF); transactions; PostgreSQL/MySQL overview; DBA responsibilities, operational lifecycle and use cases | Master Index + Database Fundamentals |
| 02. Linux, OS and installation prerequisites | Linux navigation and permissions; users/groups; processes/services; CPU/RAM/swap; filesystems, mounts, disk/IOPS; package managers/repos/RPM dependencies; network basics; DNS, routes, firewall, SELinux; sizing and capacity pre-checks | Master Index + Installation |
| 03. PostgreSQL installation and configuration | Repository and RPM installation; package verification; initdb/PGDATA; systemd service; directories and config files; version/port/listen settings; reload vs restart; parameter context and precedence; Windows installation awareness; offline/air-gapped installation; rollback and installation troubleshooting | Master Index + Installation |
| 04. PostgreSQL architecture and internals | Process model; postmaster/backend; connection lifecycle; parser/rewriter/planner/executor; shared/local memory; shared_buffers, WAL buffers, work_mem, maintenance_work_mem, temp_buffers; WAL, checkpoints, crash recovery; MVCC, xmin/xmax; background processes; PGDATA and storage layout; write/read paths | Master Index + Architecture |
| 05. psql, pgAdmin and DBA utilities | psql connection/meta-commands; pgAdmin server registration/query tool/backup/monitoring; DBeaver; CLI vs GUI trade-offs; explain plans; export/import; safe production usage | Master Index + GUI & DBA Tools |
| 06. SQL fundamentals | DDL/DML/DQL/DCL/TCL; CREATE/ALTER/DROP/TRUNCATE; INSERT/UPDATE/DELETE/SELECT; WHERE, ORDER BY, LIMIT; aggregates, GROUP BY, HAVING; NULL; casts; constraints; transaction basics | Master Index; supplement SQL practice |
| 07. Advanced SQL and database objects | Joins; subqueries; CTEs/recursive CTEs; window functions; views/materialized views; sequences/identity; functions/procedures/triggers; JSON/JSONB; arrays; extensions; query patterns and SQL review | Master Index |
 
### Level 2 — Core database administration

| Topic | Required coverage | Source alignment |
|---|---|---|
| 08. Database/schema/object/tablespace administration | Create/alter/drop databases; templates; ownership; schemas/search_path; tablespaces; object dependencies; database/table/index size; provisioning and decommissioning | Master Index |
| 09. Roles, privileges and access governance | Roles/users/groups; LOGIN/NOLOGIN; attributes; RBAC; memberships/inheritance/SET ROLE; GRANT/REVOKE; default privileges; object ownership; role cleanup; connection limits; least privilege | Master Index + User Management & Security |
| 10. Authentication and connectivity | pg_hba.conf first-match rules; peer, SCRAM, certificate, LDAP/PAM/GSSAPI concepts; pg_ident; local socket vs TCP; hostssl/TLS; DNS/firewall/routing; remote access; client/app connectivity; connection diagnosis | Master Index + Installation + Security |
| 11. Configuration management | postgresql.conf, auto.conf, pg_hba.conf, pg_ident.conf; SHOW/ALTER SYSTEM/pg_settings/pg_file_settings; context and precedence; reload/restart; pending_restart; safe change/rollback; resource parameter risk | Master Index + Installation |
| 12. Transactions, MVCC and concurrency | ACID in practice; BEGIN/COMMIT/ROLLBACK/savepoints; isolation levels; snapshots; locks and lock queues; blocking/deadlocks; long-running transactions; XID wraparound; pg_stat_activity/pg_locks; safe cancel/terminate | Master Index + Architecture |
| 13. Storage, vacuum and maintenance | Heap pages/tuples/TOAST; visibility map/free space map; indexes and bloat; dead tuples; VACUUM/ANALYZE/VACUUM FULL/REINDEX/CLUSTER; autovacuum thresholds/workers; freeze and wraparound prevention; table growth; partition maintenance | Master Index + Architecture + Performance |

### Level 3 — Backup, recovery, performance and operations

| Topic | Required coverage | Source alignment |
|---|---|---|
| 14. Backup and restore | Logical vs physical; pg_dump/pg_dumpall/pg_restore; custom/directory/plain formats; parallel dump/restore; pg_basebackup; cluster/database/schema/table/partition restore; CSV COPY; retention; checksums/validation; restore drills; backup security | Master Index + Backup & Recovery |
| 15. WAL, archiving and PITR | WAL segments/LSNs; checkpoints; archive_mode/archive_command; archive verification; base backup + WAL chain; recovery configuration/targets; timeline/history; PITR drills; RPO/RTO; WAL growth and archive failure response | Master Index + Backup & Recovery + Architecture |
| 16. Indexing and query optimization | B-tree, Hash, GIN, GiST, SP-GiST, BRIN; composite/unique/partial/expression/covering indexes; selectivity; sequential/index/bitmap/index-only scans; EXPLAIN/EXPLAIN ANALYZE/BUFFERS; planner statistics; joins; query rewrites; index bloat and unused/duplicate indexes | Master Index + Performance |
| 17. Performance diagnosis and tuning | Establish baseline; CPU/RAM/swap/disk/network; pg_stat_activity/database/io; pg_stat_statements; shared_buffers/work_mem/effective_cache_size/maintenance_work_mem; connections/pooling; WAL/checkpoint/autovacuum tuning; temp files; lock contention; workload-specific tuning and rollback | Master Index + Performance |
| 18. Monitoring, logging and alerting | PostgreSQL logs/log_line_prefix/slow query logging; statistics views; pgBadger; Prometheus and postgres_exporter; Grafana dashboards; alert thresholds; disk/WAL/connection/replication alerts; capacity forecasting; daily health-check runbooks | Master Index + GUI & DBA Tools + DBA Overview |
| 19. Connection pooling and workload governance **(added)** | PgBouncer; session vs transaction pooling; pool sizing; application connection storms; timeouts; workload isolation; connection limits; queueing and saturation | Gap identified against supplied PDFs |
| 20. Replication slots and WAL retention operations **(expanded)** | Physical/logical slots; confirmed_flush_lsn/restart_lsn; inactive/stale slots; WAL retention; slot invalidation; safe slot lifecycle; monitoring and disk safeguards | Master Index + Replication |

### Level 4 — Replication, resilience and enterprise operations

| Topic | Required coverage | Source alignment |
|---|---|---|
| 21. Physical/streaming replication | Primary/standby; base backup; WAL sender/receiver; streaming; async/sync; quorum sync; hot standby; lag; slots; cascading; delayed standby; promotion/rebuild; monitoring and troubleshooting | Master Index + Replication |
| 22. Logical replication and migrations | Publisher/subscriber; publications/subscriptions; replica identity; initial sync; sequences/schema/DDL limitations; conflict handling; monitoring; version migration; cutover/reconciliation; supported third-party bidirectional options | Master Index + Replication + Upgrades |
| 23. High availability and failover | Planned switchover/unplanned failover; promotion; fencing; split-brain prevention; quorum/consensus; Patroni; etcd/Consul; HAProxy/load balancers; VIP/DNS; rejoin/rebuild; failback; failover testing | Master Index |
| 24. Security, auditing and compliance | Least privilege; SCRAM; TLS/certificates; secrets/rotation; pg_hba hardening; RLS; pgaudit/audit logging; encryption at rest/in transit; security logging; privilege review; incident response | Master Index + User Management & Security |
| 25. Partitioning and large-scale data design | Range/list/hash; partition pruning; partitionwise operations; constraints/indexes; attach/detach; retention/archive; default partitions; partition maintenance automation; migration of large tables | Master Index |
| 26. Upgrades, migration and capacity planning | Minor vs major; pg_upgrade check/copy/link; pg_dumpall/logical migration; logical replication migration; extension compatibility; config review; ANALYZE after upgrade; rollback; application validation; capacity forecasting and cutover plan | Master Index + both Upgrade PDFs |
| 27. Production troubleshooting and incident management | Service startup/crash; connection exhaustion; auth failures; slow SQL; CPU/memory/I/O; locks/deadlocks; disk full; WAL/archive; replication lag; corruption suspicion; backup restore; incident severity, evidence, RCA, corrective/preventive action | Master Index + DBA Overview |
| 28. Automation and DBA scripting | Bash/SQL/Python automation; health checks; backup/retention/restore validation; cron/systemd timers; log rotation; alert hooks; idempotency; exit codes; retries; secrets handling; audit trail; Ansible basics | Master Index |
| 29. Cloud, containers and managed PostgreSQL **(added)** | RDS/Aurora and other managed PostgreSQL concepts; parameter/option groups; managed backups/replicas; cloud networking/IAM; monitoring; maintenance windows; Docker fundamentals; Kubernetes/operator awareness; limits vs self-managed control | Gap identified against supplied PDFs |
| 30. PostgreSQL ecosystem and extensions **(added)** | Extension lifecycle and compatibility; pg_stat_statements; pgcrypto; PostGIS awareness; postgres_fdw; dblink; pg_repack; pgBackRest; Barman; WAL-G; pgBouncer; pgaudit; extension upgrade and supportability | Gap identified against supplied PDFs |
| 31. Final production DBA project and interview readiness | Build multi-node lab; roles/schemas/data/indexes; backup/PITR; physical and logical replication; HA/failover design; monitoring; automation; incident simulations; runbooks; documentation; mock interviews and final assessment | Master Index |

**How to interpret the expanded numbering:** The original 26 topics remain the baseline syllabus. The consolidated map reorganizes some related areas into 31 learning modules for clarity. Nothing from the original 26 is dropped. The progress tracker will continue to reference the original 26 topic IDs unless we explicitly map a new module.

## 3. Additional gaps to close

The uploaded PDFs are useful reference notes, but they do not constitute a complete hands-on DBA course. Add the following explicit labs and competency checks:

1. Linux DBA foundations: systemd, journalctl, process signals, ulimit, vmstat, iostat, sar, lsblk, LVM, mount, permissions, SELinux, firewall, DNS and network troubleshooting.
2. SQL practice dataset: joins, grouping, window functions, CTEs, transactions, indexes, constraints and realistic query plans.
3. Connection pooler: install/configure PgBouncer; compare session and transaction pooling; validate prepared statement and session-state caveats.
4. Backup engineering: pgBackRest or Barman; full/differential/incremental strategy as supported by selected tool; encryption, retention, repository checks, restore validation and DR drill.
5. PostgreSQL internals: system catalogs, statistics, relation files, page inspection concepts, WAL/LSN, MVCC visibility, vacuum freeze and checkpoint behaviour.
6. HA operations: Patroni + consensus store, HAProxy, fencing, failover/failback, rejoin and split-brain tabletop exercise.
7. Security labs: RLS, TLS verification, certificate rotation, pgaudit, secret handling, role/privilege audit and security incident response.
8. Ecosystem labs: extensions, FDW, pg_repack, pg_stat_statements, pgBadger, Prometheus exporter and Grafana.
9. Cloud/containers: managed PostgreSQL operational differences, Docker-based disposable lab and Kubernetes/operator concepts.
10. Operational excellence: SLI/SLO, alert quality, runbooks, change management, patch windows, capacity planning, incident communications and post-incident RCA.
11. Data migration: CSV/COPY, schema migration/versioning, large-table migration, validation/reconciliation and rollback.
12. Testing: pgbench workload generation, concurrency tests, restore-time measurement, replication-lag tests and controlled failure drills.

## 4. Important corrections and safety review of the PDFs

Use the PDFs as study material, but do not execute every example literally. The following require correction or version-specific verification before a lab:

- **Never remove all PostgreSQL packages with a broad wildcard** such as `yum remove postgresql* -y` on a host that may contain another cluster or dependent package. Inventory packages, services, data directories and backups first.
- **Do not disable SELinux or use broad `trust` authentication as a standard fix.** Prefer correct SELinux labels/ports and SCRAM/TLS with narrow HBA rules.
- **Do not open 5432 to `0.0.0.0/0` as a default.** Restrict firewall and HBA access to approved source networks.
- **Do not copy a live PGDATA directory using ordinary tar/cp/rsync as a valid physical backup.** Use a cleanly stopped cold copy or supported online backup tooling such as pg_basebackup/pgBackRest/Barman, with the required WAL strategy.
- **A physical backup is cluster-level, not a direct single-table restore.** Use logical backup or restore to a temporary cluster and extract the required object.
- **Synchronous replication is not a blanket guarantee of zero data loss in every failover.** Durability depends on synchronous mode, quorum/standby configuration, promotion policy and the actual acknowledged standby state.
- **Native logical replication is not a general bidirectional multi-master solution and does not automatically replicate all DDL/schema changes.** Plan schema changes separately; use a specifically supported external solution if bidirectional writes are required.
- **Do not assume a fixed shared_buffers percentage, 99% cache-hit target, or a universal max_connections value is correct.** Baseline the workload and size based on memory, concurrency, query patterns and operating-system cache.
- **Do not treat effective_cache_size as allocated/reserved memory.** It is a planner estimate.
- **Do not run destructive restore, upgrade, failover or role-cleanup commands without a verified backup, dependency inventory, maintenance plan and rollback criteria.**
- **Verify PostgreSQL 17/18 feature claims against the exact server version and official release documentation.** In particular, treat claims about native DDL replication, bidirectional replication, and new parameters/features as unverified until confirmed.
- **The GUI/DBA tools PDF mixes PostgreSQL tools with MySQL-oriented Percona Toolkit examples.** Keep MySQL-only utilities clearly labelled and do not assume they are PostgreSQL administration tools.

## 5. Required lesson format

Every lesson must contain:
1. Plain-English concept and real-world analogy.
2. Why a DBA needs it and how it works internally.
3. Safe step-by-step lab using the actual active lab version.
4. Exact Linux/SQL commands and explanation of each command.
5. Expected output and validation query.
6. Common errors, diagnosis and safe remediation.
7. Production DBA scenario and operational safeguards.
8. Interview questions with concise model answers.
9. Assignment and completion criteria.

Do not mark a practical complete until the learner shares output and it is reviewed. Keep a clear distinction between **read**, **explained**, **practised**, and **production-ready**.

## 6. Current learner lab and sequencing

The latest active learning thread uses **VILASLAB1 / PostgreSQL 18.4**, with service `postgresql-18`, data directory `/var/lib/pgsql/18/data`, config `/var/lib/pgsql/18/data/postgresql.conf`, and training database `dba_training`. A separate earlier lab record used `postgresql-lab1` / PostgreSQL 17.11; do not mix paths or service names between them.

The learner is currently in Topic 01, covering primary keys, foreign keys, constraints and relationships. The departments/employees lab practical and deliberate constraint-failure checks are pending review. Next lesson after verification: ACID, normalization and transactions.

## 7. Ongoing GitHub maintenance

After each learning session:
- Update the relevant topic README with only what was actually taught.
- Add commands and outputs only after the learner runs them.
- Append a dated entry to `DAILY-ACTIVITY.md`.
- Update status/evidence in `learning-progress.md`.
- Never store passwords, tokens, private keys, real production data or sensitive connection strings.
