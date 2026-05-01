---
title: "Docker Overlay Network"
tags: [docker, networking, overlay]
source: "https://docs.docker.jp/engine/userguide/networking/dockernetworks.html"
created: 2026-05-01
related: [docker-container-networking, docker-bridge-network, container-service-discovery]
---

# Docker Overlay Network

Docker overlay networking is a multi-host virtual network model that lets containers on different Docker hosts communicate as if they were on the same private network.

## How It Works

An overlay network builds a logical Layer 2/Layer 3 communication plane above physical host networks. Docker encapsulates container traffic so packets can move between hosts while preserving the abstraction of one shared network. From the container perspective, services appear to be on a common network segment even when they run on separate machines.

Overlay networking depends on cluster-aware control mechanisms that distribute network state across participating nodes. In older Docker architectures this often involved external key-value stores and explicit daemon configuration, while modern Docker stack usage integrates overlay behavior with orchestrated service deployment patterns. In both cases, network membership, endpoint information, and service reachability must be coordinated across hosts.

Compared with bridge networking, overlay networks target cross-host communication rather than single-host isolation. Containers attached to the same overlay can typically resolve and connect to peer services without requiring manual host-level routing per application. This makes overlay a core building block for distributed container systems.

## Why It Matters

As soon as workloads span more than one host, single-host bridge networks are no longer sufficient. Overlay networking provides the communication substrate needed for distributed microservices, scalable deployments, and fault-tolerant scheduling across nodes.

It also improves portability of service architecture. Teams can keep service-level connectivity rules consistent while scaling horizontally, instead of rebuilding network topology each time containers move to another host. This supports cleaner operations, smoother environment parity, and simpler service-to-service communication in clustered platforms.

## Related Concepts

[[docker-container-networking]] provides the broader taxonomy of Docker network types and isolation models. [[docker-bridge-network]] explains local single-host networking, which overlay extends beyond one machine. [[container-service-discovery]] covers name resolution and service lookup patterns used within distributed container networks.
