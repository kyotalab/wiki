---
title: "Docker Bridge Network"
tags: [docker, networking, bridge]
source: "https://docs.docker.jp/engine/userguide/networking/dockernetworks.html"
created: 2026-05-01
related: [docker-container-networking, docker-overlay-network, container-service-discovery]
---

# Docker Bridge Network

Docker bridge networking is a single-host virtual network model that connects containers through a software bridge while isolating them from external networks unless ports are explicitly published.

## How It Works

A bridge network creates an internal Layer 2 segment on the Docker host, where each attached container receives a private IP address from the bridge subnet. Docker installs routing and network address translation (NAT) rules so containers can reach outbound networks, while inbound access from outside the host is blocked by default unless port mappings are configured.

Docker includes a legacy default bridge (`docker0`), but user-defined bridge networks are generally preferred. With user-defined bridges, containers in the same network can communicate more predictably, and Docker provides built-in DNS-based name resolution for service names on that network. This removes much of the manual linking behavior that older workflows depended on.

Bridge networks are host-local by design. They are effective for multi-container applications running on one machine, where services need internal communication boundaries and selective external exposure. When cross-host communication is required, bridge networking is usually combined with other approaches such as overlay networking.

## Why It Matters

Bridge networking provides a practical default security boundary for containerized development and small production deployments. Teams can run multiple services on one host, isolate internal traffic, and publish only required interfaces, which reduces accidental exposure.

It also improves operational clarity. By grouping related containers into user-defined bridge networks, developers gain stable service naming, cleaner environment setup, and fewer ad hoc connectivity fixes. This makes local development, testing, and troubleshooting more repeatable before scaling to multi-host architectures.

## Related Concepts

[[docker-container-networking]] gives the broader model across default, user-defined, and multi-host network types. [[docker-overlay-network]] extends connectivity across hosts when bridge scope is no longer sufficient. [[container-service-discovery]] explains name resolution and service lookup inside container networks.
