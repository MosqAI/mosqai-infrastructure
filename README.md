# mosqai-infrastructure

Everything needed to run MosqAI Shield outside a single developer's editor:
Docker Compose stacks, the MQTT broker config (TLS + per-device ACL), shared CI/CD
workflows, environment separation (dev / staging / prod), backups, and
monitoring/logging.

Primary owner: Developer 1, with Developer 2 on the broker and device provisioning.

## Technology

Docker · Docker Compose · Eclipse Mosquitto · PostgreSQL · GitHub Actions ·
(later) a reverse proxy with automatic HTTPS

## Setup

> Not scaffolded yet. First M0 issue: "Local dev stack".
> **Docker Desktop is not installed on the current machine yet.**

Planned:

```bash
cp .env.example .env
docker compose -f compose.dev.yml up -d   # postgres, mosquitto, (later) backend, ai
```

## Environment variables

See [`.env.example`](.env.example). Staging and production values live in GitHub
Environments or the host's secret store, never in this repo.

## Environments

| Env | Purpose | Data |
| --- | --- | --- |
| dev | Local machines | Disposable, seeded |
| staging | Pre-release integration with real devices | Test data only |
| production | Real users and devices | Backed up daily; restores tested |

## Testing

CI validates compose files and runs backend integration tests against this stack.

## Deployment

Documented per environment as each one is created.

## Contribution workflow

Branch from `develop` (`feature/…`, `fix/…`, `refactor/…`), use Conventional
Commits, open a PR into `develop`, one approval. Full rules:
[mosqai-docs/workflow.md](https://github.com/MosqAI/mosqai-docs/blob/develop/workflow.md).
