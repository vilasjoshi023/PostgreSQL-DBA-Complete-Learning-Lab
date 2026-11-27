# PostgreSQL DBA Complete Learning Lab

A hands-on, beginner-to-advanced PostgreSQL DBA learning repository, grounded in the PostgreSQL DBA Master Index and the learner's uploaded reference PDFs.

## Learning approach

The curriculum follows the source syllabus in sequence. The consolidated review and expanded map is documented in [CURRICULUM-REVIEW-AND-EXPANSION.md](CURRICULUM-REVIEW-AND-EXPANSION.md).

Each lesson includes:
- Plain-English concepts and internal architecture
- Why the feature matters to a DBA
- Safe hands-on Linux and SQL exercises
- Exact commands, expected output and verification
- Troubleshooting and safe remediation
- Production scenarios and interview answers
- Assignment and completion criteria

**Progress rule:** A topic is not marked practised/completed until the learner runs the practical and shares output for review.

## Lab environments

The latest active learning thread uses **VILASLAB1 / PostgreSQL 18.4**:
- Service: `postgresql-18`
- Data directory: `/var/lib/pgsql/18/data`
- Main config: `/var/lib/pgsql/18/data/postgresql.conf`
- Training database: `dba_training`

A separate earlier lab record used **postgresql-lab1 / PostgreSQL 17.11**. Keep its history separate; never reuse its paths or service name for VILASLAB1.

See [LAB-ENVIRONMENT.md](LAB-ENVIRONMENT.md) and verify the live server before running version-specific commands.

## Curriculum and progress

- [Curriculum review and expanded learning map](CURRICULUM-REVIEW-AND-EXPANSION.md)
- [Learning progress tracker](learning-progress.md)
- [Daily learning journal](DAILY-ACTIVITY.md)
- [Topic folder index](TOPIC-FOLDER-INDEX.md)

The original 26-topic syllabus remains the progress-tracking baseline. Additional learning modules and gaps are mapped in the curriculum review document.

## Repository safety

- Never commit database passwords, tokens, private keys, credential-bearing connection strings or production data.
- Use lab-only credentials.
- Do not use broad `trust` authentication or open database ports to all networks.
- Back up configuration files before editing.
- Distinguish reloadable parameters from restart-only parameters.
- Do not run destructive commands against production without an approved change plan and verified recovery path.
- Treat sample parameter values in training PDFs as examples, not universal production recommendations.
