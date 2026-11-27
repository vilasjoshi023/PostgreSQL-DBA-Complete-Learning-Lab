# Topic 04 — psql and pgAdmin

**Status: Partial**

## Syllabus
- Connect and disconnect using psql.
- Essential psql meta-commands.
- Inspect databases, schemas, tables and database objects.
- Register a server in pgAdmin and use Query Tool.
- Troubleshoot connection and authentication errors.

## Confirmed psql practice
- Connected to `dba_training`.
- Used `\l`, `\dn`, `\dt`, `\dp`, `\du`, `\ddp` and `\q`.
- Used `SHOW` to inspect server settings.
- Inspected schemas, tables, privileges and roles.

## Command reference

```text
\l          list databases
\c DBNAME   connect to database
\dn         list schemas
\dt         list tables
\dt *.*     list tables across schemas
\du         list roles
\dp         show table privileges
\ddp        show default privileges
\conninfo   show current connection
\q          quit psql
\h          SQL command help
\?          psql meta-command help
```

## Remaining
- pgAdmin installation and server registration practical.
- Query Tool and object browser.
- Export/import and connection troubleshooting in pgAdmin.
- psql variables, output formatting and scripting options.
