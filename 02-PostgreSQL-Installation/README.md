# Topic 02 — PostgreSQL Installation and Prerequisites

**Status: Practised; formal runbook expansion remains.**

## Syllabus
- Linux prerequisites: RAM, CPU, disk and filesystem checks.
- PostgreSQL packages, repositories and version compatibility.
- Installation on CentOS Stream/RHEL-compatible Linux.
- initdb, data directory and service startup.
- systemctl, package verification and troubleshooting.
- Safe installation validation.

## Confirmed lab
- OS: CentOS Stream 9.
- PostgreSQL: 17.11.
- Service unit: `postgresql-17`.
- Data directory: `/var/lib/pgsql/17/data`.
- Service was verified active and enabled during the lab.
- VM observed with 2 vCPU and approximately 2.7 GiB RAM.

## Useful verification commands

```bash
cat /etc/centos-release
free -h
nproc
df -h
rpm -qa | grep '^postgresql17' | sort
psql --version
systemctl status postgresql-17
systemctl is-enabled postgresql-17
```

## Still to document/practise
- Full clean-install sequence with repository setup and package dependencies.
- initdb options and data-directory ownership.
- Disk/filesystem planning and mount considerations.
- Installation failure scenarios and recovery.
- Post-install security baseline and acceptance checklist.

> Re-check live package and service state before applying these notes to another VM.
