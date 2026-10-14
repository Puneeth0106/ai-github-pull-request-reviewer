# Publication validation

The following checks were performed on the prepared files. These are static checks, not a claim that the complete application runs successfully.

## Completed

- Parsed and compiled all 16 Python source files without importing their dependencies.
- Parsed 22 YAML files, one JSON dashboard, and the Alembic INI configuration.
- Validated `compose.yaml` using `docker compose config --quiet` with placeholder environment values. The temporary `.env` used for this check was removed.
- Checked Compose dependency names, Dockerfile paths, Docker `COPY` source paths, workflow triggers, and local reusable-workflow references.
- Checked that `.env.example` covers every application settings field and that its local database URL matches its PostgreSQL initialization values.
- Checked README relative links against files on disk. The supplied upstream repository link was reachable through the browsing tool.
- Checked ignore rules for the original archive, Git metadata backup, credentials, dotenv files, virtual environments, caches, and Terraform state/variable values. Example configuration and Terraform provider lockfiles remain eligible for version control.
- Scanned publishable text for common private-key/API-token patterns and exact credential values extracted from the supplied Secret, including its database password and private-key body. No matches remained outside the ignored backup. This is a targeted scan, not a full secret-scanner or vulnerability audit.
- Inspected the supplied architecture image and retained it as a design reference.
- Confirmed all 23 retained files under `services/` are byte-for-byte identical to the downloaded bundle. Removed only the five deployment-trigger marker files; application code was not modified.
- Inspected the archive for license/copyright notices. No license file, copyright statement, or SPDX notice was included.

## Not tested

- Container image builds or stack startup: the Docker CLI and Compose were available, but no Docker daemon was running.
- Service imports or application tests: required packages including Celery, asyncpg, Langfuse, and the Prometheus instrumentator were not available in the current Python environment; no application test suite was supplied.
- Terraform formatting, validation, or plans: the Terraform executable was unavailable. Terraform files were reviewed as text only.
- Kubernetes server-side schema validation, cloud provisioning, migrations against PostgreSQL, queue delivery, GitHub webhook/review posting, model calls, tracing, monitoring, or Ragas evaluation.
- GitHub Actions execution: workflows were reviewed and parsed locally, not executed by GitHub.

## Publication environment

The workspace restricted writes to `.git`, so the prepared Git metadata was stored in the ignored `_local_backup/git-metadata/` directory. GitHub CLI authentication reported an invalid stored token and the CLI could not connect to `api.github.com`. Repository creation, public visibility, metadata updates, and pushing could not be verified in this environment. Local continuation instructions are kept in the ignored backup folder.
