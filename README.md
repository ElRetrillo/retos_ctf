# retos_ctf

Official challenge repository for the **EclipSec CTF** platform (<https://eclipsec.cl>).

Each challenge is self-contained, runs **locally** on the participant's machine with Docker,
and is described by a machine-readable `eclipsec.yaml` manifest that the EclipSec backend
uses to register it. Challenges are downloaded on demand by the **EclipSec CLI**.

```
retos_ctf/
├── README.md
├── CONTRIBUTING.md
├── .gitignore
└── web/                      # category
    └── sqli-001/             # one challenge = one directory
        ├── eclipsec.yaml     # metadata (id, name, category, difficulty, points, target)
        ├── Dockerfile
        ├── compose.yaml
        ├── README.md         # player-facing: how to run/stop. NO solution, NO flag.
        └── src/              # challenge source (intentionally vulnerable)
```

## Layout rules

- **One challenge per directory**, grouped by category (`web/`, `crypto/`, `pwn/`, `forensics/`, `misc/`, ...).
- The directory path (e.g. `web/sqli-001`) is the `path` the backend stores and the CLI downloads.
- Every challenge **must** ship a valid `eclipsec.yaml`, a `Dockerfile`, a `compose.yaml` and a player `README.md`.
- A challenge must run with a single `docker compose up --build` and expose the port declared in `eclipsec.yaml`.

## Running a challenge locally

```bash
cd web/sqli-001
docker compose up --build      # start (see each challenge's port)
docker compose down            # stop
```

Or, once the CLI is installed:

```bash
eclipsec challenge start web-sqli-001
eclipsec challenge stop  web-sqli-001
```

## Security

- This repo is **public** so the CLI can download challenges without credentials.
- Challenges are **intentionally vulnerable** — run them only in disposable, isolated environments.
- Never commit production secrets, backend credentials, GitHub tokens or user data here.
- A challenge may contain its own flag locally (that is the point); the authoritative flag for
  scoring lives in the EclipSec backend, never in the public API responses.

See [CONTRIBUTING.md](CONTRIBUTING.md) to add a challenge.
