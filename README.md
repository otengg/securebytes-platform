# SecureBytes Platform

> A self-hosted platform operated as the internal infrastructure for a one-person company. Every service is treated as production.

[![Status](https://img.shields.io/website?url=https%3A%2F%2Fstatus.securebytes.net%2Fstatus%2Flab&label=platform&style=flat-square)](https://status.securebytes.net/status/lab)
[![Build](https://img.shields.io/badge/build-month_1_of_6-blue?style=flat-square)](#)
[![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)](LICENSE)

![Architecture](docs/architecture/architecture.svg)

## Overview

Nine internal services behind nginx with wildcard TLS, two public services via Cloudflare Tunnel with identity-aware proxy on the admin surface, and a fourteen-monitor observability stack with push alerting. The architecture diagram above shows the five-layer structure; solid boxes are live, dashed boxes are planned.

## Current footprint

| Layer | Live | Planned |
| --- | --- | --- |
| Edge | Cloudflare Tunnel, Cloudflare Access | — |
| Ingress | cloudflared, nginx + wildcard TLS | Authentik, step-ca |
| Platform | — | k3s HA cluster (Cilium, Linkerd, ArgoCD) |
| Data | Vaultwarden | CloudNativePG, Redis, MinIO, Vault |
| Observability | Grafana, Uptime Kuma | VictoriaMetrics, Loki, Tempo, Pyrra |
| Infrastructure | Two-node Proxmox cluster, NAS, pfSense | Proxmox Backup Server |

## Live

The platform's public status page is monitored continuously and exposes uptime for every component above the infrastructure layer.

[status.securebytes.net/status/lab](https://status.securebytes.net/status/lab)