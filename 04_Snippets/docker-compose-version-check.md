---
title: "Check Docker Compose Version"
tags: [docker, compose, migration]
source: "https://docs.docker.com/compose/, https://docs.docker.com/compose/migrate/"
created: 2026-05-01
related: [compose-v2-migration]
---

# Check Docker Compose Version

Detects whether Compose V2 (`docker compose`) or legacy Compose V1 (`docker-compose`) is available and prints version details.

## Code

```bash
#!/usr/bin/env bash
set -euo pipefail

if ! command -v docker >/dev/null 2>&1; then
  echo "Error: docker command is not installed." >&2
  exit 1
fi

echo "Checking Docker Engine..."
docker --version

echo ""
echo "Checking Compose availability..."
if docker compose version >/dev/null 2>&1; then
  echo "Compose V2 detected:"
  docker compose version
elif command -v docker-compose >/dev/null 2>&1; then
  echo "Legacy Compose V1 detected:"
  docker-compose --version
  echo "Recommendation: migrate scripts to 'docker compose' syntax."
else
  echo "Error: No Compose command found." >&2
  echo "Install Docker Compose plugin or Docker Desktop." >&2
  exit 1
fi
```

## Usage Notes

- Save as `check-compose-version.sh`, then run `chmod +x check-compose-version.sh && ./check-compose-version.sh`.
- Use this in CI or setup scripts to fail fast when Compose is missing.
- If only `docker-compose` is found, plan migration to `docker compose` for long-term consistency.
- When both commands exist, standardize team docs and automation on Compose V2.
- For workflow context, see [[compose-v2-migration]] and [[docker-vs-docker-compose-workflows]].

## Related

- [[compose-v2-migration]] — Explains why teams move from `docker-compose` to `docker compose`.
- [[docker-vs-docker-compose-workflows]] — Places version checks in practical development workflows.
