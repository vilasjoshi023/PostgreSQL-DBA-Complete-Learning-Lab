# Topic 10 — Authentication and Connectivity

**Status: In progress**

## Goal

Understand how a client connects to PostgreSQL and how PostgreSQL decides whether to accept the connection.

Simplified flow:

Client → listening server address/port → matching pg_hba.conf rule → authentication → database session.

## Current lab HBA configuration

The learner inspected these active, non-comment HBA entries:

```conf
local   all             all                                     peer
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             ::1/128                 scram-sha-256
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256
```

Interpretation:
- `local` refers to Unix-domain socket connections.
- `host` refers to TCP connections.
- `peer` uses the operating-system identity for local authentication.
- `scram-sha-256` requires PostgreSQL password authentication over these localhost TCP rules.
- `127.0.0.1/32` is IPv4 loopback.
- `::1/128` is IPv6 loopback.

Command run:

```bash
grep -vE '^[[:space:]]*(#|$)' /var/lib/pgsql/17/data/pg_hba.conf
```

## Next controlled tests (not yet confirmed as executed)

Peer test, from Linux account postgres:

```bash
psql -d dba_training
```

Inside psql:

```sql
SELECT current_user;
SELECT current_database();
\q
```

SCRAM TCP test:

```bash
psql -h 127.0.0.1 -U dba_user -d dba_training -W
```

PostgreSQL postgres role over TCP (only if a valid lab password is configured):

```bash
psql -h 127.0.0.1 -U postgres -d dba_training -W
```

## Key rule

PostgreSQL evaluates applicable `pg_hba.conf` rules from top to bottom and uses the first matching rule. An authentication failure does not mean PostgreSQL tries the next rule.

## Remaining curriculum
- Run and compare peer vs SCRAM tests.
- Understand `host`, `hostssl`, `hostnossl`, `reject`, `trust` and HBA ordering.
- Learn firewall, DNS, routing and listen-address checks.
- Test a controlled connection from another VM.
- Learn TLS/SSL and certificate validation.
- Test application-style connectivity.

## Security
Never add broad `trust` rules in production. Do not expose passwords in shell history, Git, or shared logs.
