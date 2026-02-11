# Vaultwarden Containerised

---

## Overview

A self-hosted password & secret management deployment using [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (Bitwarden-compatible server) optimised for Apple Silicon / ARM64 architecture. This turns your M-series Mac Mini/Studio into a powerful professional (headless) home/studio server.

Originally forked from [dadatuputi/bitwarden_gcloud](https://github.com/dadatuputi/bitwarden_gcloud), replaced and minimised external dependencies with [CloudFlare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel) protection, and redesigned for on-premise ARM-based servers using MacOS native [Apple/Container](https://github.com/apple/container) via [Container Compose](https://github.com/container-compose/cli).

## Why This Stack?

- **Zero-trust networking**: CloudFlare Tunnel eliminates port forwarding and direct internet exposure
- **ARM-optimised**: Native ARM64 images for better performance on Apple Silicon (Mac Mini M2/M4)
- **Low maintenance**: Watchtower keeps containers automatically updated
- **Privacy-focused**: Your data stays on your hardware

## Features

- Bitwarden self-hosted (via [Vaultwarden](https://github.com/dani-garcia/vaultwarden)) 
- Runs using [Apple/Container](https://github.com/apple/container) via [Container Compose](https://github.com/container-compose/cli)
- Secure external access via [CloudFlare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel) (no port forwarding required)
- Automatic container updates via Watchtower

## Prerequisites

- [Apple/Container](https://github.com/apple/container) installed
- [Container Compose](https://github.com/container-compose/cli) installed
- CloudFlare account with a configured tunnel

## Getting Started

1. Pull all required images:

```bash
container image pull vaultwarden/server:latest-alpine
container image pull cloudflare/cloudflared:latest
container image pull containrrr/watchtower:latest
```

2. Configure your environment:

```bash
cp .env.template .env
```

Edit `.env` and set at minimum:
- `DOMAIN`: Your fully-qualified domain (e.g., `https://vault.example.com`)
- `TUNNEL_TOKEN`: Your CloudFlare Tunnel token
- `TZ`: Your timezone (e.g., `Etc/UTC`)

3. Start the services:

```bash
container-compose up -d
```

## Services

- `bitwarden`: Vaultwarden server (port 80)
- `tunnel`: CloudFlare Tunnel for secure external access
- `watchtower`: Automatic container updates (runs Sundays at 3am by default)

## Configuration

See `.env.template` for all available configuration options including:
- SMTP settings for email invitations
- Push notification settings
- Yubikey 2FA configuration
- Organization creation restrictions
