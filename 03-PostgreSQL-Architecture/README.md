# Topic 03 — PostgreSQL Architecture

**Status: Partial**

## Syllabus
- Client-server architecture.
- Postmaster/main server and backend processes.
- Shared memory and background processes.
- shared_buffers, WAL buffers and operating-system cache.
- Checkpoints, WAL writer, background writer and autovacuum.
- Data-directory structure and storage files.

## Confirmed learning so far
- Introduced the PostgreSQL client/server model and high-level architecture.
- Identified the lab data directory and server configuration paths.

## Still to learn and validate
- Follow a client connection from startup to backend process.
- Inspect PostgreSQL processes using Linux tools.
- Understand shared memory and per-process memory.
- Trace a write through shared buffers, WAL and data files.
- Explain checkpoints, background writer and WAL writer roles.
- Inspect the data directory safely and identify key files.
- Understand autovacuum worker processes.

## Useful first-look commands

```bash
ps -ef | grep '[p]ostgres'
ps -ef | grep '[p]ostmaster'
```

```sql
SHOW data_directory;
SHOW shared_buffers;
SHOW wal_buffers;
SELECT pid, backend_type, state, usename, datname
FROM pg_stat_activity;
```

Do not manually modify or delete PostgreSQL data-directory files.
