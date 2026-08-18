---
title: "DockTail — Containers as Tailscale Services"
source: "https://docktail.org/"
author:
  - "[[marvinvr]]"
published:
created: 2026-04-21
description: "Automatically expose Docker containers as Tailscale Services using label-based configuration. Zero-config service mesh for your dockerized services."
tags:
  - "clippings"
---
## Unleash your Containers as Tailscale Services

Add labels to your Docker containers. DockTail handles the rest.

```
1

2

3

4

5

6

7

8
```
```
services:

  myapp:

    image: nginx:latest

    # No ports needed!

    labels:

      - "docktail.service.enable=true"
      - "docktail.service.name=myapp"
      - "docktail.service.port=80"
```

https://myapp.tailnet.ts.net

Service is live

myapp.tailnet.ts.net

Tailscale HTTPS

### Auto Discovery

Monitors Docker events in real-time. Start a labeled container and it appears on your Tailnet within seconds.

### Direct IP Proxy

No port publishing required. Routes directly to container IPs on the Docker network, adapting automatically on restart.

### Funnel Support

Expose any container to the public internet via Tailscale Funnel. One label takes you from private to public.

How it works

1

Add `docktail.*` labels to your container

2

DockTail detects and advertises to Tailscale

3

Access via `service.tailnet.ts.net`