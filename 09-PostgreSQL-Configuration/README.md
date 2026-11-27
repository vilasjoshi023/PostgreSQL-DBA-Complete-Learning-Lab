# Topic 09 — PostgreSQL Configuration

**Status: Practised**

## Configuration files

| File | Purpose |
|---|---|
| `postgresql.conf` | Main server configuration |
| `pg_hba.conf` | Client authentication rules |
| `pg_ident.conf` | User-name mapping for applicable authentication setups |
| `postgresql.auto.conf` | Values written by ALTER SYSTEM; can override main-file values |

Lab paths:
- Main config: `/var/lib/pgsql/17/data/postgresql.conf`
- HBA: `/var/lib/pgsql/17/data/pg_hba.conf`
- Ident: `/var/lib/pgsql/17/data/pg_ident.conf`
- Data: `/var/lib/pgsql/17/data`

## Inspection

```sql
SHOW config_file;
SHOW hba_file;
SHOW ident_file;
SHOW data_directory;
SHOW port;
SHOW listen_addresses;
SHOW max_connections;
SHOW shared_buffers;
SHOW work_mem;
SHOW maintenance_work_mem;
SHOW effective_cache_size;
```

Inspect effective source and file settings:

```sql
SELECT name, setting, source, sourcefile, sourceline
FROM pg_settings
WHERE name IN ('max_connections', 'shared_buffers', 'work_mem');

SELECT sourcefile, sourceline, name, setting, applied, error
FROM pg_file_settings
WHERE name IN ('max_connections', 'shared_buffers', 'work_mem')
ORDER BY seqno;
```

## ALTER SYSTEM and reload practical

Executed in the lab:

```sql
ALTER SYSTEM SET work_mem = '8MB';
SELECT pg_reload_conf();
SHOW work_mem;
ALTER SYSTEM RESET work_mem;
SELECT pg_reload_conf();
SHOW work_mem;
```

Observed result: after reload, work_mem changed to 8MB; after reset and another reload, it returned to the 4MB default.

## Restart-only parameter practical

Executed in the lab:
1. Set `max_connections` to 150 using ALTER SYSTEM.
2. Inspected the setting and learned it has postmaster/restart context.
3. Restarted `postgresql-17` using Linux root, not the postgres OS account.
4. Verified `SHOW max_connections` returned 150.
5. Reset the ALTER SYSTEM override and restarted.
6. Verified the value returned to 100.

```sql
ALTER SYSTEM SET max_connections = '150';
SHOW max_connections;
ALTER SYSTEM RESET max_connections;
```

A reload alone does not apply this restart-only setting.

## Configuration precedence practical

Practised:
- Session-level `SET work_mem` and `RESET work_mem`.
- Database-level `ALTER DATABASE dba_training SET work_mem = '12MB'`.
- Role-level `ALTER ROLE postgres SET work_mem = '20MB'`.
- Session-level override to 30MB.
- Verified role-specific setting took precedence over database setting for postgres; a different role received the database value.
- Reset test role/database work_mem settings and preserved database search_path.

Priority observed for these settings:
**Session > role-in-database > database > server configuration/default.**

## Operational reminders
- Check `pg_settings.context` and `pending_restart` before planning a restart.
- Back up config files before manual editing.
- Use reload only for parameters that support it.
- Restart-only settings require a controlled restart.
- Record before/after values and have a rollback plan.
- Never add broad `trust` rules in production.
- Do not grant superuser to ordinary application or employee accounts.

## Remaining review
- Config includes, environment/service options and full precedence.
- `listen_addresses`, port and remote client connection configuration.
- Safe memory sizing for production.
- Change-control documentation and rollback drill.
