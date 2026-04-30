# API Reference

Base URL (local): `http://127.0.0.1:8030`

## Health and Readiness

1. `GET /health`
2. `GET /ready`
3. `GET /healthz` (alias for `/health`)
4. `GET /readyz` (alias for `/ready`)

Readiness behavior:

1. Returns `200` with `status=ready` when sqlite dependency is available.
2. Returns `503` with `status=not_ready` when dependencies are unavailable.

## Authentication

When `NEURALSCOPE_API_KEY` is configured, protected HTTP endpoints require `X-API-Key`.

Protected endpoints:

1. `POST /api/v1/models/parse`
2. `POST /api/v1/models/analyze`
3. `GET /api/v1/sessions`
4. `GET /api/v1/sessions/{session_id}`

Unauthenticated probe endpoints:

1. `/`
2. `/health`, `/ready`, `/healthz`, `/readyz`
3. `/docs`, `/openapi.json`, `/redoc`

## Model Graph

1. `POST /api/v1/models/parse`

Request body:

1. `model_name` (string)
2. `payload` (object)

## Signal Analysis

1. `POST /api/v1/models/analyze`

Request body:

1. `model_name` (string)
2. `graph` (object)
3. `metrics` (object)

## Sessions

1. `GET /api/v1/sessions`
2. `GET /api/v1/sessions/{session_id}`
3. `GET /ws/sessions/{session_id}` (websocket stream)

## Request Guard Controls

1. Host header enforcement via `NEURALSCOPE_ALLOWED_HOSTS`.
2. Max payload guard via `NEURALSCOPE_MAX_PAYLOAD_BYTES`.
3. Per-client fixed-window rate limiting via `NEURALSCOPE_RATE_LIMIT_PER_MINUTE`.

## Error Contract

All HTTP failures return a normalized envelope:

```json
{
	"error": {
		"code": "string",
		"message": "string",
		"request_id": "string",
		"details": []
	}
}
```

Common error codes:

1. `bad_request`
2. `unauthorized`
3. `not_found`
4. `payload_too_large`
5. `validation_error`
6. `rate_limited`
7. `internal_error`

Rate limit response:

1. Status `429`
2. Error code/message: `rate_limited`
3. Includes `Retry-After: 60` response header

All responses include request correlation and security headers:

1. `X-Request-ID`
2. `X-Content-Type-Options: nosniff`
3. `X-Frame-Options: DENY`
