# web-sqli-001 — Login Bypass (intentionally vulnerable)
FROM python:3.12-slim

# Pin the runtime dependency for reproducible builds
RUN pip install --no-cache-dir flask==3.1.0

# Run as an unprivileged user
RUN useradd --create-home --uid 10001 ctf
WORKDIR /app
COPY --chown=ctf:ctf src/ .
USER ctf

EXPOSE 8080

# Readiness probe: the login page must respond on :8080
HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=5 \
  CMD python -c "import urllib.request,sys; sys.exit(0 if urllib.request.urlopen('http://127.0.0.1:8080/').status==200 else 1)"

CMD ["python", "app.py"]
