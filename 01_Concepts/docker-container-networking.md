---
title: "Docker Container Networking"
tags: [docker, networking, containers]
source: "https://docs.docker.jp/engine/userguide/networking/dockernetworks.html"
created: 2026-04-30
related: [docker-bridge-network, docker-overlay-network, container-service-discovery]
---

# Docker Container Networking

Docker container networking is the model Docker uses to isolate containers and control how they communicate with each other, the host, and external systems.

## How It Works

Docker provides three built-in default networks: `bridge`, `host`, and `none`. If no network is specified at container startup, Docker connects the container to the default `bridge` network (`docker0`). On this network, containers can reach each other by IP address, but name-based discovery is limited in the legacy default bridge model unless older linking behavior is used.

User-defined networks improve this behavior and are the preferred approach for most real workloads. A user-defined `bridge` network creates an isolated communication boundary on a single host while allowing controlled port publishing to external clients. Containers attached to the same user-defined bridge can typically discover and talk to each other more predictably than on the legacy default bridge.

For multi-host communication, Docker supports `overlay` networks. Overlay networking connects containers across different Docker hosts so services can communicate as if they were on one logical network. This requires cluster-aware setup and coordination components, and in older Docker models may depend on external key-value stores and host-level port configuration.

Docker also includes an internal DNS service for user-defined networks, allowing container name resolution and service discovery without manual host mapping. When internal resolution is not possible, requests can be forwarded to upstream DNS. In parallel, Docker supports plugin-based network drivers, so teams can integrate custom networking behavior beyond built-in drivers.

## Why It Matters

Containerized systems depend on clear network boundaries. Docker networking provides those boundaries while keeping connectivity configurable, which is essential for both security and operability. Teams can isolate application tiers, reduce accidental cross-service access, and expose only the ports that are required.

Networking mode also affects architecture choices. Single-host apps often work well with user-defined bridges, while distributed systems need overlay-style connectivity and stronger service discovery patterns. Understanding these trade-offs helps avoid brittle setups based on legacy linking and supports more maintainable, production-ready container platforms.

## Related Concepts

[[docker-bridge-network]] covers single-host isolation and port exposure behavior. [[docker-overlay-network]] explains multi-host virtual networking and cluster prerequisites. [[container-service-discovery]] describes DNS-driven name resolution between services.
