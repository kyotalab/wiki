---
title: "Launch Services from docker-compose.yaml"
tags: [docker, compose, workflow]
source: "https://docs.docker.com/reference/cli/docker/compose/up/, https://docs.docker.com/reference/compose-file/"
created: 2026-05-01
related: [docker-vs-docker-compose-workflows, compose-v2-migration]
---

# Launch Services from docker-compose.yaml

Starts a multi-service stack from `docker-compose.yaml`, verifies service status, and tails logs for quick troubleshooting.

## Code

```bash
#!/usr/bin/env bash
set -euo pipefail

COMPOSE_FILE="docker-compose.yaml"

if ! command -v docker >/dev/null 2>&1; then
  echo "Error: docker command is not installed." >&2
  exit 1
fi

if ! docker compose version >/dev/null 2>&1; then
  echo "Error: docker compose (Compose V2) is not available." >&2
  exit 1
fi

if [[ ! -f "${COMPOSE_FILE}" ]]; then
  echo "Error: ${COMPOSE_FILE} not found in the current directory." >&2
  exit 1
fi

echo "Validating compose file..."
docker compose -f "${COMPOSE_FILE}" config >/dev/null

echo "Starting services in background..."
docker compose -f "${COMPOSE_FILE}" up -d --remove-orphans

echo "Current service status:"
docker compose -f "${COMPOSE_FILE}" ps

echo ""
echo "Recent logs (last 100 lines per service):"
docker compose -f "${COMPOSE_FILE}" logs --tail 100
```

## Usage Notes

- Save as `compose-up.sh`, then run `chmod +x compose-up.sh && ./compose-up.sh`.
- Run this script from the directory that contains `docker-compose.yaml`.
- Use `docker compose -f docker-compose.yaml down` to stop and remove the stack.
- Replace `logs --tail 100` with `logs -f` when you want live streaming logs.
- For migration and workflow guidance, see [[compose-v2-migration]] and [[docker-vs-docker-compose-workflows]].

## Related

- [[docker-vs-docker-compose-workflows]] — Explains why declarative Compose workflows are better for multi-service setups.
- [[compose-v2-migration]] — Covers command syntax and compatibility between V1 and V2.
