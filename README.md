<div align="center">

# SecureBytes Platform

A self-hosted platform for network and security infrastructure.

[![Platform Status](https://img.shields.io/website?url=https%3A%2F%2Fstatus.securebytes.net%2Fstatus%2Flab&label=platform&style=flat-square&color=3fb950)](https://status.securebytes.net/status/lab)

![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=flat-square&logo=proxmox&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![nginx](https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![pfSense](https://img.shields.io/badge/pfSense-212121?style=flat-square&logo=pfsense&logoColor=white)
![Let's Encrypt](https://img.shields.io/badge/Let's_Encrypt-003A70?style=flat-square&logo=letsencrypt&logoColor=white)

</div>

---

![Architecture](docs/architecture/architecture.svg)

---

## Overview

Internal services behind nginx with wildcard TLS, a public status page via Cloudflare Tunnel, and a fourteen-monitor observability stack with push alerting. The architecture diagram above shows the five-layer structure; solid boxes are live, dashed boxes are deferred or later decisions.

## Current Footprint

<table>
<thead>
<tr>
<th align="left">Layer</th>
<th align="left">Live</th>
<th align="left">Planned</th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Edge</b></td>
<td>Cloudflare Tunnel · Cloudflare Access</td>
<td>—</td>
</tr>
<tr>
<td><b>Ingress</b></td>
<td>cloudflared · nginx + wildcard TLS</td>
<td>Authentik · step-ca</td>
</tr>
<tr>
<td><b>Platform</b></td>
<td>LXC services (Vaultwarden, nginx, observability)</td>
<td>k3s HA cluster (Cilium, Linkerd, ArgoCD) — later explicit decision</td>
</tr>
<tr>
<td><b>Data</b></td>
<td>Vaultwarden</td>
<td>CloudNativePG · Redis · MinIO · Vault</td>
</tr>
<tr>
<td><b>Observability</b></td>
<td>Grafana · Uptime Kuma</td>
<td>VictoriaMetrics · Loki · Tempo · Pyrra</td>
</tr>
<tr>
<td><b>Infrastructure</b></td>
<td>Two-node Proxmox · NAS (file share, not PBS)</td>
<td>—</td>
</tr>
</tbody>
</table>

## Live Status

The platform's public status page is monitored continuously and exposes uptime for every component above the infrastructure layer.

<div align="center">

[**status.securebytes.net/status/lab →**](https://status.securebytes.net/status/lab)

</div>