# Operations Guide

## Routine Checks

1. API health/readiness are green.
2. Parse and analyze endpoints return expected metrics.
3. Session history updates after each analysis run.

## Recovery

1. Restart backend service.
2. Verify sqlite path permissions.
3. Re-run known payload for sanity checks.

## Smoke Commands

```bash
cd backend
pytest -q

cd ../frontend
npm run build
```
