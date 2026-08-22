---
type: Architecture Decision
title: ADR-0003 Parameterise the API host instead of hard-coding it
description: Every request targets a HOST environment variable so the same collection runs against sandbox, paper or production.
status: accepted
date: 2022-08-04
deciders: []
supersedes: []
affects: [alpaca_postman.broker_collection, alpaca_postman.trader_collection, alpaca_postman.market_data_collection, ext_broker_api, ext_trader_api, ext_market_data_api]
allium: []
evidence: ["Postman Collections/Broker_API.json", "Postman Collections/Trader_v2_API.json", "Postman Collections/Market_Data_v2_API.json", "README.md"]
tags: [alpacahq, adr, generated]
timestamp: 2026-08-21T21:43:34Z
generated_by: claude-opus-5 / layered-docs 2026-08
source_commit: ad68ba8e7a79725108f8df68cc4a12e9f01d6a75
source_branch: allium/layered-docs-2026-08
generated_at: 2026-08-21T21:43:34Z
confidence: medium
review_status: draft-needs-review
---

# ADR-0003 Parameterise the API host instead of hard-coding it

## Context
The same request set has to run against more than one environment: the Broker collection documents a sandbox and a
production host, and the Trader collection documents a paper and a production host, each in a table inside the
collection description (`Postman Collections/Broker_API.json`, `Postman Collections/Trader_v2_API.json`). The README
tells a newcomer that the sample environment already carries a sandbox host value and that switching to production means
changing the host and obtaining different keys (`README.md`).

## Decision
Request URLs are written against a `{{HOST}}` variable supplied by the developer's Postman environment rather than an
absolute base URL. The variable appears 118 times in the Broker export, 64 times in the Market Data export and 59 times
in the Trader export, and no collection-level variable pins a default (`Postman Collections/*.json`).

## Consequences
- One collection covers sandbox, paper and production; the environment alone decides which one is hit (`README.md`).
- Nothing runs until the environment is configured, so the README makes the Clock or Calendar request the smoke test (`README.md`).
- Because no default is stored in the collections, the host values live only in the sample environment, which is not part of this repository — a reader cloning the repository alone cannot tell which host a request would reach.
- Credentials are parameterised the same way, in two schemes: the Broker collection's collection-level basic auth reads `{{api_key}}` / `{{api_secret}}`, while the Trader v2 and Market Data v2 collections send per-request `Apca-Api-Key-Id` / `Apca-Api-Secret-Key` headers bound to the `{{APCA_API_KEY_ID}}` / `{{APCA_API_SECRET_KEY}}` environment variables (`Postman Collections/Broker_API.json`, `Postman Collections/Trader_v2_API.json`, `Postman Collections/Market_Data_v2_API.json`).

## Alternatives considered
Not recorded in the repository.
