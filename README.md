<div align="center">

# SecureBytes Platform

A self-hosted platform for network and security infrastructure.

[![Platform Status](https://img.shields.io/website?url=https%3A%2F%2Fstatus.securebytes.net%2Fstatus%2Flab&label=platform&style=flat-square&color=3fb950)](https://status.securebytes.net/status/lab)
[![Write-up](https://img.shields.io/badge/write--up-securebytes.net-3fb950?style=flat-square&labelColor=0d1117)](https://securebytes.net/projects/securebytes-platform/)

![Proxmox](https://img.shields.io/badge/Proxmox-E57000?style=flat-square&logo=proxmox&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)
![nginx](https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![pfSense](https://img.shields.io/badge/pfSense-212121?style=flat-square&logo=pfsense&logoColor=white)
![Let's Encrypt](https://img.shields.io/badge/Let's_Encrypt-003A70?style=flat-square&logo=letsencrypt&logoColor=white)

</div>

---

![Architecture](docs/architecture/architecture.svg?v=4)

---

## Overview

Internal services run as containers and VMs on a two-node Proxmox cluster. nginx terminates a wildcard certificate. The firewall is the DNS authority. Sign-in is a lab directory. Remote access is a separate path from that sign-in. Visitors can open the status page. The rest of the lab is private, reached through a Cloudflare Tunnel with no inbound ports. House Wi-Fi is its own network and has no route into the lab. New guests are built with Terraform. Ansible is grouped by role.

## What is running

<table>
<thead>
<tr>
<th align="left">Layer</th>
<th align="left">Live</th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Edge</b></td>
<td>Cloudflare Tunnel · Cloudflare Access · public status page</td>
</tr>
<tr>
<td><b>Ingress</b></td>
<td>cloudflared · nginx + wildcard TLS · Unbound on the firewall</td>
</tr>
<tr>
<td><b>Identity</b></td>
<td>Lab directory for internal sign-in. Remote access stays its own path.</td>
</tr>
<tr>
<td><b>Platform</b></td>
<td>Vault · directory · reverse proxy · SIEM · network sensor</td>
</tr>
<tr>
<td><b>Observability</b></td>
<td>Grafana · Prometheus · push alerts · Uptime Kuma · Splunk · Security Onion</td>
</tr>
<tr>
<td><b>Segments</b></td>
<td>Lab · management · IoT · DMZ · house Wi-Fi. House Wi-Fi has no route into the lab.</td>
</tr>
<tr>
<td><b>Infrastructure</b></td>
<td>Two-node Proxmox · firewall · switch · Wi-Fi 7 AP · NAS file share</td>
</tr>
<tr>
<td><b>Build</b></td>
<td>Terraform for new guests · Ansible by role</td>
</tr>
</tbody>
</table>

Cisco modeling stays powered off unless there is a lab window. It is not part of the always-on platform. The NAS is a file share. It is not a backup host.

## What raises it next

These are the unfinished pieces. A Kubernetes cluster, a second metrics stack, and backup software on the NAS are not the plan.

- Hardening scores on every container, taken before and after the change.
- Copies that still exist if the hypervisor is lost.
- Sign-in groups decide who gets a remote path.
- A practice range on its own segment. It never shares the lab network.

## Live status

<div align="center">

[**status.securebytes.net/status/lab →**](https://status.securebytes.net/status/lab)

[**Project write-up on securebytes.net →**](https://securebytes.net/projects/securebytes-platform/)

</div>
