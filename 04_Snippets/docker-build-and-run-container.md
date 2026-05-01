---
title: "Build and Run a Docker Container"
tags: [docker, container, workflow]
source: "https://www.seeds-std.co.jp/blog/creators/2023-06-21-183202/, https://docs.docker.com/reference/cli/docker/container/run/"
created: 2026-05-01
related: [docker-vs-docker-compose-workflows]
---

# Build and Run a Docker Container

Builds a local image from a `Dockerfile` and runs a named container with basic safety checks.

## Code

```bash
#!/usr/bin/env bash
set -euo pipefail

IMAGE_NAME="my-app:dev"
CONTAINER_NAME="my-app-dev"
HOST_PORT="8080"
CONTAINER_PORT="8080"

if [[ ! -f "Dockerfile" ]]; then
  echo "Error: Dockerfile not found in the current directory." >&2
  exit 1
fi

if ! command -v docker >/dev/null 2>&1; then
  echo "Error: docker command is not available." >&2
  exit 1
fi

if ! docker info >/dev/null 2>&1; then
  echo "Error: Docker daemon is not running." >&2
  exit 1
fi

echo "Building image: ${IMAGE_NAME}"
docker build -t "${IMAGE_NAME}" .

if docker ps -a --format '{{.Names}}' | rg -x "${CONTAINER_NAME}" >/dev/null; then
  echo "Removing existing container: ${CONTAINER_NAME}"
  docker rm -f "${CONTAINER_NAME}" >/dev/null
fi

echo "Starting container: ${CONTAINER_NAME}"
docker run -d \
  --name "${CONTAINER_NAME}" \
  -p "${HOST_PORT}:${CONTAINER_PORT}" \
  --restart unless-stopped \
  "${IMAGE_NAME}"

echo "Container is running."
docker ps --filter "name=${CONTAINER_NAME}" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

## Usage Notes

- Save as `run-container.sh`, then run `chmod +x run-container.sh && ./run-container.sh`.
- Change `IMAGE_NAME`, `CONTAINER_NAME`, and port variables for your service.
- This script force-removes an existing container with the same name before recreating it.
- If your app needs environment variables or volume mounts, add `-e` and `-v` flags to `docker run`.
- For multi-service local environments, prefer Compose patterns in [[docker-vs-docker-compose-workflows]].

## Related

- [[docker-vs-docker-compose-workflows]] — Shows when imperative `docker run` workflows are enough and when to move to Compose.
- [[docker-containers]] — Covers container lifecycle basics used by this snippet.
