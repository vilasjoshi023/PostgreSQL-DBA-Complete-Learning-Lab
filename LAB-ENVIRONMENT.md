# PostgreSQL Lab Environment

## Current active learning VM

| Property | Current recorded value |
|---|---|
| Hostname | VILASLAB1 |
| OS | CentOS Stream 9 (current learning context) |
| PostgreSQL | 18.4 |
| Service | `postgresql-18` |
| Service state | Active/running and enabled in the latest confirmed session |
| Data directory | `/var/lib/pgsql/18/data` |
| Port | 5432 (verify live before use) |
| Main config | `/var/lib/pgsql/18/data/postgresql.conf` |
| Training database | `dba_training` |
| VM resources | 2 vCPU; approximately 3.5 GiB RAM as recorded for this lab VM |

## Verification commands

Run these before a lab, especially after VM or package changes:

```bash
hostnamectl
cat /etc/centos-release
free -h
nproc
df -h
psql --version
systemctl status postgresql-18
systemctl is-active postgresql-18
systemctl is-enabled postgresql-18
```

Connect as the PostgreSQL operating-system account:

```bash
su - postgres
psql -d dba_training
```

Or execute a one-shot query:

```bash
su - postgres -c "psql -d postgres -c 'SELECT version();'"
```

Verify server properties:

```sql
SELECT version();
SHOW port;
SHOW data_directory;
SHOW config_file;
SHOW hba_file;
SHOW ident_file;
SHOW listen_addresses;
SHOW max_connections;
SHOW shared_buffers;
SHOW work_mem;
```

## Earlier separate lab — do not mix with current lab

An earlier repository record used:
- Hostname: `postgresql-lab1`
- PostgreSQL: 17.11
- Service: `postgresql-17`
- Data directory: `/var/lib/pgsql/17/data`

This is historical context only. Do not use PG17 service names or file paths on VILASLAB1.

## Resource and operational safety

The current VM has limited memory. Treat all tuning values as lab examples only. `effective_cache_size` is a planner estimate, not reserved memory. Do not copy production-sized settings from PDFs into this small VM.

Before editing configuration:
1. Verify hostname, server version, service and config path.
2. Save a timestamped copy of the configuration file.
3. Change one parameter at a time.
4. Check syntax and pending-restart status.
5. Reload or restart only as required.
6. Verify the effective value and record rollback steps.

Never store passwords, tokens, private keys or credential-bearing connection strings in Git.
