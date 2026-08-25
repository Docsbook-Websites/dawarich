---
title: "Self-Hosting Dawarich"
description: "Install Dawarich on Docker, Kubernetes, Synology, Unraid or Home Assistant, then configure, monitor and maintain your own instance."
---

# Self-Hosting Dawarich

Self-hosting Dawarich is free and includes every feature of the paid plans. What it asks in return is that you run the database, keep the instance reachable and handle upgrades — all of which is documented here.

<!-- widget:cards -->

## Install

- [Self-Hosting Introduction](./introduction.md) — Get started self-hosting Dawarich with Docker and Docker Compose, including prerequisites and setup {server}
- [Hardware Requirements](./hardware-requirements.md) — Minimum hardware requirements for self-hosting Dawarich, including RAM, CPU, and disk space recommendations {cpu}
- [Installation](./installation/docker.md) — Install Dawarich using Docker and Docker Compose on Linux, macOS, Windows, or Synology {container}
- [Docker Compose](./installation/docker-compose.md) — Set up Dawarich using Docker Compose by following the self-hosting introduction guide {layers}
- [Install Dawarich on Kubernetes](./installation/kubernetes.md) — Deploy Dawarich on a Kubernetes cluster with YAML manifests {hexagon}
- [Synology](./installation/synology.md) — Step-by-step guide to install and configure Dawarich on a Synology NAS using Container Manager {hard-drive}
- [Unraid](./installation/unraid.md) — A guide on how to install Dawarich on Unraid using Community Applications (CA) plugin {hard-drive}
- [Home Assistant](./installation/home-assistant.md) — Run Dawarich as a native Home Assistant app with automatic location tracking {house}

## Configure

- [Environment Variables and Settings](./environment-variables.md) — Reference for all Dawarich environment variables including database, Redis, geocoding, and application {sliders-horizontal}
- [Setting Up Reverse Proxy](./configuration/reverse-proxy.md) — Configure a reverse proxy with Nginx, Traefik, Caddy, or Apache for your self-hosted Dawarich instance {shield}
- [Exposing via CloudFlare Tunnel](./configuration/cloudflare-tunnel.md) — Expose your self-hosted Dawarich instance to the internet using CloudFlare Zero Trust Tunnels without {cloud}
- [OIDC Authentication](./configuration/oidc-authentication.md) — Configure OpenID Connect (OIDC) authentication with providers like Authentik, Authelia, or Keycloak for {key-round}
- [Configuring SMTP](./configuration/smtp.md) — Configure outgoing email (password reset, digests, family invitations) for your self-hosted Dawarich {mail}
- [Reverse Geocoding](./configuration/reverse-geocoding.md) — Configure reverse geocoding in Dawarich using Photon, Geoapify, Nominatim, or a self-hosted service to {globe}

## Maintain

- [Updating Guides](./updating.md) — Breaking changes and migration instructions for each Dawarich version update {refresh-cw}
- [Backup & Restore](./maintenance/backup-and-restore.md) — Back up and restore your Dawarich PostgreSQL database using Docker commands {archive}
- [Updating to PostgreSQL 17 with PostGIS](./maintenance/update-postgresql.md) — Step-by-step guide to upgrade your Dawarich database from an older PostgreSQL version to PostgreSQL 17 {database}
- [Moving to PostGIS](./maintenance/moving-to-postgis.md) — Migrate your Dawarich database from standard PostgreSQL to PostGIS for spatial data support {database}
- [Monitoring with Prometheus](./monitoring/prometheus.md) — Export Dawarich metrics to Prometheus for monitoring your self-hosted instance {activity}
- [The Watcher](./monitoring/watcher.md) — Automatically import GPX, OwnTracks, and GeoJSON files by watching a directory for new files {eye}

<!-- /widget -->

## Running on ARM64?

Dawarich runs on AMD64 and ARM64 alike. If `docker compose` fails to pull with `no matching manifest for linux/arm64/v8`, it is the database image rather than Dawarich — [Moving to PostGIS](./maintenance/moving-to-postgis.md) lists the replacement image for each architecture.

## Related

- [Move a self-hosted instance to cloud](../cloud/migrate-from-self-hosted.md)
- [Community questions](../community-questions.md)
