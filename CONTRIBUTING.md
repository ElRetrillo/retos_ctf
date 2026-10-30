# Contributing a challenge

A challenge is a self-contained directory under a category folder. To add one:

## 1. Pick an id and path

- **id**: `<category>-<name>-<nnn>`, e.g. `web-sqli-001`. Globally unique.
- **path**: `<category>/<name>-<nnn>`, e.g. `web/sqli-001`. This is what the backend stores
  and the CLI downloads.

## 2. Create the directory

```
web/sqli-001/
├── eclipsec.yaml
├── Dockerfile
├── compose.yaml
├── README.md
└── src/
```

## 3. Write `eclipsec.yaml`

```yaml
id: web-sqli-001            # unique, matches the backend registry
name: Login Bypass
version: "1.0"
category: web               # web | crypto | pwn | forensics | misc
difficulty: easy            # easy | medium | hard | insane
points: 100                 # informational; the backend is the source of truth
author: EclipSec
description: Short, spoiler-free summary.
target:
  type: http                # http | tcp
  port: 8080                # the port compose.yaml publishes
```

## 4. Dockerfile rules

- Pin the base image and runtime dependency versions.
- **Run as a non-root user.**
- Do **not** use `--privileged`, bind `/var/run/docker.sock`, or `network_mode: host`.
- Add a `HEALTHCHECK` so tooling can detect readiness.

## 5. compose.yaml rules

- Publish only the port from the manifest.
- Set `read_only`, drop capabilities and disable privilege escalation where possible.

## 6. README.md rules (player-facing)

Document name, id, category, difficulty, points, objective, how to run, port, how to stop.
**Do NOT include the solution, the exploit payload, or the flag.**

## 7. Flags

- The flag may live inside the challenge environment (so the player can find it).
- Flag format: `EclipSec{...}`.
- The authoritative flag for scoring must also be registered in the EclipSec backend seed.
- Never expose the flag through any public API response or public documentation.

## 8. Test before opening a PR

```bash
cd web/sqli-001
docker compose up --build        # resolve it yourself end-to-end
docker compose down
```
