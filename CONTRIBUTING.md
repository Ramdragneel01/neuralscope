# Contributing

## Setup

1. Install Python 3.12+ and Node.js 20+.
2. Copy `.env.example` to `.env`.
3. Install backend/frontend dependencies.
4. Run tests and build before pull requests.

## Validation

```bash
cd backend
pytest -q

cd ../frontend
npm run build
```

## PR Requirements

1. Keep each PR focused and testable.
2. Update docs for API/deployment changes.
3. Add clarification notes for non-obvious design trade-offs.
