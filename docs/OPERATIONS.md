# Operations Guide

## Routine Checks

1. API health/readiness are green.
2. Parse and analyze endpoints return expected metrics.
3. Session history updates after each analysis run.
4. Error responses contain `error.code`, `error.message`, and `error.request_id`.
5. `429` responses include `Retry-After` when ingress bursts exceed policy.

## Recovery

1. Restart backend service.
2. Verify sqlite path permissions.
3. Re-run known payload for sanity checks.
4. If sustained `429` errors appear, tune `NEURALSCOPE_RATE_LIMIT_PER_MINUTE`.

## Smoke Commands

```bash
cd backend
pytest -q

cd ../frontend
npm run build
```

## Incident Triage

1. Confirm probes via `/healthz` and `/readyz`.
2. Inspect logs using `X-Request-ID` from failed client responses.
3. Validate host header policy for reverse proxy `Host` forwarding.
4. Confirm API clients are sending `X-API-Key` when auth is enabled.
