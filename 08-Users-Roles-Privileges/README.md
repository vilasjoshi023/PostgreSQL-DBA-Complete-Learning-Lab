# Topic 08 — Users, Roles and Privileges

**Status: Practised; some advanced team-role work remains to be validated.**

## Concepts covered

- PostgreSQL roles can be login identities or group roles.
- `LOGIN` enables a role to authenticate.
- Database `CONNECT`, schema `USAGE`, and table privileges are separate permission layers.
- `GRANT` adds privileges; `REVOKE` removes granted privileges.
- Default privileges affect future objects created by the specified owner; they do not retroactively grant access to existing objects.
- Role membership supports group-based access management.
- Least privilege means granting only the access needed for a job.

## Lab roles

- `dba_user` — login role used for permission testing.
- `reporting_user` — read-oriented login role.
- `developer_role` — group role.
- `developer_user1` — login role granted membership in developer_role.

A team-role design using `dba_team`, `developer_team` and `testing_team` plus employee-style logins was discussed, but execution is not confirmed. Do not treat those proposed accounts as created.

## Example lab commands

```sql
CREATE ROLE dba_user WITH LOGIN PASSWORD '<set-lab-password-securely>';
GRANT CONNECT ON DATABASE dba_training TO dba_user;
GRANT USAGE ON SCHEMA dba_training TO dba_user;
GRANT SELECT, INSERT, UPDATE, DELETE
ON ALL TABLES IN SCHEMA dba_training TO dba_user;
```

Use a secure password method; do not put passwords in source control or shared notes.

Test from a client:

```bash
psql -h localhost -U dba_user -d dba_training -W
```

Permission inspection:

```sql
\du
\dp
\ddp
```

## DML permission test performed

- Connected as dba_user.
- Inserted a test employee row and deleted it.
- As the owner/admin role, revoked INSERT, UPDATE and DELETE on the employees table.
- Verified SELECT continued to work while write attempts were denied.

## Default privileges lesson

Example:

```sql
ALTER DEFAULT PRIVILEGES FOR ROLE postgres IN SCHEMA dba_training
GRANT SELECT ON TABLES TO reporting_user;
```

Default privileges affect future objects created by the named role. Existing tables need a separate GRANT.

## Production guardrails

- Do not use superuser for application accounts.
- Separate ownership/admin roles from application login roles.
- Prefer group roles and job-based grants.
- Test allowed and denied operations.
- Review schema, table, sequence and function privileges separately.
- Check object ownership before deleting roles.
