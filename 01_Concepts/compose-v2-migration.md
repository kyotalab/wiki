---
title: "Compose V2 Migration"
tags: [docker, compose, migration]
source: "https://docs.docker.com/compose/migrate/, https://docs.docker.com/compose/"
created: 2026-04-30
related: [docker-vs-docker-compose-workflows, docker-cli-command-structure, docker-container-networking]
---

# Compose V2 Migration

Compose V2 migration is the transition from the legacy standalone `docker-compose` (Compose V1) command to the modern `docker compose` subcommand integrated into the Docker CLI.

## How It Works

Compose V1 was distributed as a separate Python-based tool with its own command binary, while Compose V2 is implemented as a Docker CLI plugin. In practice, this changes the command style from hyphenated `docker-compose` to spaced `docker compose`, aligning Compose operations with the same command tree used for images, containers, networks, and other Docker objects.

Most compose files and common lifecycle commands remain conceptually similar. Teams still define services declaratively in `compose.yaml` or `docker-compose.yml`, then use commands such as `up`, `down`, and `logs` to control multi-container applications. The migration effort is often centered on command syntax updates in local workflows, shell scripts, CI pipelines, and team documentation rather than a full redesign of service definitions.

Because Compose V2 is part of the Docker CLI ecosystem, it benefits from more consistent option behavior, plugin-based distribution, and improved integration with Docker Desktop and modern Docker Engine tooling. Existing environments may temporarily keep `docker-compose` as a compatibility command, but long-term maintenance typically favors standardizing on `docker compose`.

## Why It Matters

Standardizing on Compose V2 reduces fragmentation in developer workflows. A single CLI surface lowers onboarding friction, makes operational commands easier to remember, and avoids confusion caused by mixed V1 and V2 usage across environments.

Migration also improves reliability in shared automation. When teams update scripts and documentation to one canonical command form, they reduce subtle failures in CI/CD and local setup. More broadly, adopting V2 keeps Compose aligned with Docker's current development direction, which lowers future upgrade risk.

## Related Concepts

[[docker-vs-docker-compose-workflows]] explains when Compose should be preferred over manual container orchestration. [[docker-cli-command-structure]] shows why `docker compose` fits the unified CLI model. [[docker-container-networking]] provides context for how Compose simplifies multi-service network setup.
