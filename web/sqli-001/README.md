# Login Bypass

| | |
|---|---|
| **ID** | `web-sqli-001` |
| **Category** | web |
| **Difficulty** | easy |
| **Points** | 100 |
| **Version** | 1.0 |

## Objective

The **SecureCorp Internal Administration Portal** is protected by a login form.
Your goal is to authenticate as the **admin** user and reveal the flag shown on the
admin dashboard. Regular accounts can log in but will not see the flag.

## How to run

```bash
cd web/sqli-001
docker compose up --build
```

The portal is served at <http://localhost:8080>.

Or with the EclipSec CLI:

```bash
eclipsec challenge start web-sqli-001
```

## Port

- HTTP: **8080**

## How to stop

```bash
docker compose down
```

Or:

```bash
eclipsec challenge stop web-sqli-001
```

## ⚠️ Intentionally vulnerable

This challenge contains a deliberate security flaw for educational purposes.
Run it only in an isolated, disposable environment. Do not deploy it to the internet.
