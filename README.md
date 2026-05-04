# SecureBytes Platform

A self-hosted platform built and operated as the internal infrastructure for a one-person company. Every service is treated as production: deployed via GitOps where applicable, monitored, alerted on, and documented.

Current state: nine internal services behind nginx with wildcard TLS, two public services via Cloudflare Tunnel with identity-aware proxy on the admin surface, and a fourteen-monitor observability stack with push alerting.

See `docs/architecture/architecture.svg` for the five-layer architecture diagram. Solid boxes are live; dashed boxes are planned. Build sequence runs through October 2026.
