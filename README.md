# PostgreSQL DBA Complete Learning Lab

A hands-on, beginner-to-advanced PostgreSQL DBA learning repository. The curriculum follows the **PostgreSQL DBA Master Index** in order, with simple explanations, lab exercises, expected results, safe troubleshooting, and interview preparation.

## Learning approach

For each topic, maintain:
- Concepts and internal architecture
- Why the feature is needed and how it works
- Linux and SQL commands, with explanations
- Lab steps and expected output
- Validation and troubleshooting
- Production DBA considerations and safety checks
- Interview questions and practical assignments

Progress labels:
- **Practised** — hands-on work is confirmed in the learning record.
- **Partial** — some concepts/practicals are covered; other syllabus items remain.
- **In progress** — currently being studied.
- **Not started** — no learning activity recorded yet.

## Lab environment

| Item | Current lab |
|---|---|
| Hostname | `postgresql-lab1` |
| Operating system | CentOS Stream 9 |
| PostgreSQL | 17.11 |
| PostgreSQL service | `postgresql-17` |
| Service state | Active and enabled (last confirmed during lab) |
| Data directory | `/var/lib/pgsql/17/data` |
| Port | `5432` |
| Main configuration | `/var/lib/pgsql/17/data/postgresql.conf` |
| HBA configuration | `/var/lib/pgsql/17/data/pg_hba.conf` |
| Ident configuration | `/var/lib/pgsql/17/data/pg_ident.conf` |
| Training database | `dba_training` |
| VM resources | 2 vCPU; approximately 2.7 GiB RAM (observed in lab) |

> Lab values are recorded from terminal history; re-check live values before using them elsewhere.

## Curriculum and progress

See [learning-progress.md](learning-progress.md) for all 26 syllabus topics and the current assessment.

## Daily learning journal

See [DAILY-ACTIVITY.md](DAILY-ACTIVITY.md). Each session records the date, topic/subtopic, concepts, commands, practical outcome, errors, resolution, status, and next activity.

## Topic folders

Topics 01–26 are represented in the directory structure. Topic folders will be populated progressively as lessons and practicals are completed. A folder existing does **not** mean its topic is complete.

## Safety and secret handling

- Never commit database passwords, tokens, private keys, credential-bearing connection strings, or production data.
- Use lab-only credentials and rotate any credential that was accidentally exposed.
- Do not use broad `trust` authentication in production.
- Back up configuration files before editing them.
- Distinguish reloadable settings from restart-only settings.
- Do not run destructive commands against production without an approved change plan and verified backup.

## Current position

Topics 01–09 have been reached with varying levels of completion. Topic 10 (Authentication and connectivity) is in progress. The current known activity is inspection of `pg_hba.conf`; authentication test commands and remote-connectivity practicals remain pending.

## Repository maintenance

After each session, update the relevant topic notes, `DAILY-ACTIVITY.md`, and `learning-progress.md`. Only mark a practical completed after reviewing its actual output.
