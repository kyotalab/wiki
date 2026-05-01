---
title: "Container Service Discovery"
tags: [docker, networking, service-discovery]
source: "https://docs.docker.jp/engine/userguide/networking/dockernetworks.html, https://docs.docker.com/network/"
created: 2026-05-01
related: [docker-container-networking, docker-bridge-network, docker-overlay-network]
---

# Container Service Discovery

Container service discovery is the mechanism that lets containers find and connect to other services by stable names instead of hardcoded IP addresses.

## How It Works

In containerized environments, service instances can start, stop, and move frequently, so direct IP-based configuration quickly becomes brittle. Service discovery solves this by introducing a naming layer that maps service names to current network endpoints. Applications connect to logical names, and the platform resolves those names at runtime.

In Docker, this behavior is commonly provided through built-in DNS on user-defined networks. Containers attached to the same network can resolve peer service or container names without manual `/etc/hosts` management. This is a major shift from older patterns that relied on explicit linking and static assumptions about connectivity.

The quality of service discovery depends on network scope and orchestration model. On single-host bridge setups, discovery is limited to the relevant user-defined network boundary. In multi-host overlay-based deployments, discovery extends across nodes, enabling distributed services to communicate through consistent naming even when runtime placement changes.

## Why It Matters

Service discovery improves resilience and maintainability in distributed applications. Teams can scale services, restart containers, or redeploy components without rewriting connection settings throughout the stack.

It also simplifies developer workflows. Instead of passing dynamic IPs through scripts and environment files, developers can use stable service names, which reduces setup errors and makes local, staging, and production environments easier to keep consistent.

## Related Concepts

[[docker-container-networking]] provides the broader network model where discovery operates. [[docker-bridge-network]] explains host-local connectivity and name resolution scope. [[docker-overlay-network]] extends discovery-enabled communication across multiple hosts.
