# neuralscope Architecture

## Overview

neuralscope provides a practical debugging surface for neural model structure and signal-health diagnostics.

## Runtime Topology

1. Backend API service
   - Model graph parser
   - Activation/gradient analyzer
   - Session persistence and retrieval
2. Frontend dashboard
   - Model graph request form
   - Analysis execution form
   - Session history and summaries
3. SQLite storage
   - Captures analysis snapshots for reproducibility and comparisons

## Data Flow

1. Client submits model layer specification.
2. API returns graph nodes/edges and parameter estimates.
3. Client submits activation/gradient tensors.
4. API computes dead-neuron and vanishing-gradient ratios.
5. Session summary is persisted and shown in dashboard history.

## Security and Reliability

1. Trusted host guard.
2. Request payload size limit.
3. Optional HSTS in production.
4. Health and readiness endpoints.
5. Type-validated payload contracts.

## Scale Path

1. Replace SQLite with Postgres for team-scale history.
2. Stream live hook events over websocket channels.
3. Add large-model graph chunking and progressive rendering.
