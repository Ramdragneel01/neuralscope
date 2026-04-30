# Deployment Guide

## Local Compose

```bash
docker compose --env-file .env -f docker-compose.yml up --build
```

## Production Compose

```bash
docker compose --env-file .env -f docker-compose.prod.yml up --build -d
```

## GitHub Setup

1. Enable Pages using GitHub Actions.
2. Push semantic tags (`vX.Y.Z`) for release pipeline.

## Health Checks

1. `GET /health`
2. `GET /ready`
3. `GET /healthz`
4. `GET /readyz`

## Environment Variables

1. `NEURALSCOPE_ALLOWED_HOSTS`
2. `NEURALSCOPE_CORS_ORIGINS`
3. `NEURALSCOPE_MAX_PAYLOAD_BYTES`
4. `NEURALSCOPE_RATE_LIMIT_PER_MINUTE`
5. `NEURALSCOPE_API_KEY`
6. `NEURALSCOPE_ENABLE_HSTS`
7. `NEURALSCOPE_DB_PATH`

## Production Hardening Checklist

1. Restrict `NEURALSCOPE_ALLOWED_HOSTS` to public ingress hostnames.
2. Restrict `NEURALSCOPE_CORS_ORIGINS` to trusted frontend domains.
3. Set non-empty `NEURALSCOPE_API_KEY` for protected endpoint access.
4. Tune `NEURALSCOPE_RATE_LIMIT_PER_MINUTE` to expected traffic shape.
5. Keep `NEURALSCOPE_MAX_PAYLOAD_BYTES` minimal for your request profile.
6. Enable `NEURALSCOPE_ENABLE_HSTS=true` only behind TLS termination.
