---
title: "Docker Images"
tags: [docker, images, containers]
source: "https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/, https://docs.docker.com/engine/reference/commandline/image/"
created: 2026-05-01
related: [docker-containers, docker-cli-command-structure, docker-vs-docker-compose-workflows]
---

# Docker Images

Docker images are immutable packaged templates that define filesystem contents and runtime metadata used to create containers.

## How It Works

An image is built as a layered artifact, usually from a `Dockerfile`, where each instruction adds a read-only layer. Docker reuses cached layers across builds and across different images when possible, which accelerates build and distribution workflows. Because layers are immutable, image behavior is consistent across environments as long as the same image reference is used.

Images are commonly distributed through container registries. Teams can pull base images, add application code and dependencies, and publish versioned images with tags. A container runtime then combines the image layers with a writable container layer at startup, so runtime changes stay isolated from the original image artifact.

Image management operations include building, tagging, listing, inspecting, removing, exporting, and importing images. These lifecycle actions support repeatable release pipelines where build outputs become deployable units. In practice, image quality depends on choices such as base image selection, layer ordering, dependency pinning, and security scanning in CI.

## Why It Matters

Images are the portability contract of containerized systems. The same image can run on different developer machines, CI agents, and production hosts with minimal environment drift, which improves reproducibility and troubleshooting.

They also enable operational discipline. Versioned images make rollbacks explicit, support traceable deployments, and separate build-time concerns from runtime orchestration. This is a key reason container platforms can scale from local development to multi-environment delivery workflows.

## Related Concepts

[[docker-containers]] explains how images become running processes with writable runtime state. [[docker-cli-command-structure]] covers the command groups used to build and manage image artifacts. [[docker-vs-docker-compose-workflows]] shows how image definitions feed multi-service application setups.
