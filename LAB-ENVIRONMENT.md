# PostgreSQL Lab Environment

## Current learning VM

| Property | Recorded value |
|---|---|
| Hostname | `postgresql-lab1` |
| OS | CentOS Stream 9 |
| PostgreSQL | 17.11 |
| Service | `postgresql-17` |
| Data directory | `/var/lib/pgsql/17/data` |
| Port | 5432 |
| Main config | `/var/lib/pgsql/17/data/postgresql.conf` |
| HBA file | `/var/lib/pgsql/17/data/pg_hba.conf` |
| Ident file | `/var/lib/pgsql/17/data/pg_ident.conf` |
| Training database | `dba_training` |
| CPU | 2 vCPU |
| RAM | Approximately 2.7 GiB observed |

## Verification commands

```bash
hostnamectl
cat /etc/centos-release
free -h
nproc
df -h
psql --version
systemctl is-active postgresql-17
systemctl is-enabled postgresql-17
```

Connect as the PostgreSQL operating-system account:

```bash
su - postgres
psql -d dba_training
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

## Resource note

The VM has limited memory. Treat configuration values as learning-lab values only. `effective_cache_size` is a planner estimate, not memory reserved by PostgreSQL. Do not copy lab settings blindly into production.

## Security note

Lab credential examples have appeared in the training conversation. They are intentionally excluded from this repository. Never store real credentials in Git or shared notes.
