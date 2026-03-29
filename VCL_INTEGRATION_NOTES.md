# VCL Integration Notes

This fork is prepared for a backend-only Render deploy.

## What already works

- The backend can be deployed as a Render web service with `Dockerfile.render-backend`.
- Render can run two services from `render.yaml`:
  - `mirofish-staging`
  - `mirofish-production`
- Health is available on `/health`.

## What is still required for Virtual Consumer Lab

The current upstream API is **not** the same contract that VCL expects today.

Current upstream flow:

1. `POST /api/graph/ontology/generate`
2. `POST /api/graph/build`
3. `POST /api/simulation/create`
4. `POST /api/simulation/prepare`
5. `POST /api/simulation/start`
6. `GET /api/simulation/<id>/run-status`

Current VCL expectation:

1. `POST /api/simulations`
2. `GET /api/simulations/<id>/status`
3. `GET /api/simulations/<id>`

That means one of these must happen before a true end-to-end go-live:

- VCL backend is adapted to the upstream MiroFish workflow, or
- this fork gets a compatibility adapter that exposes the VCL contract.

## Required secrets

The current upstream validates both of these at startup:

- `LLM_API_KEY`
- `ZEP_API_KEY`

OpenAI key alone is not enough for the current upstream.
