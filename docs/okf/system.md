---
type: System
title: Alpaca Postman Collections
description: A publication repository of Postman collection exports for the public Alpaca Broker, Trader and Market Data APIs, aimed at developers evaluating or integrating those APIs.
resource: likec4://alpacahq/alpaca_postman
tags: [alpacahq, developer-experience, api-collections, generated]
status: maintenance
owners: []
timestamp: 2026-08-21T21:43:34Z
generated_by: claude-opus-5 / layered-docs 2026-08
source_commit: ad68ba8e7a79725108f8df68cc4a12e9f01d6a75
source_branch: allium/layered-docs-2026-08
generated_at: 2026-08-21T21:43:34Z
confidence: medium
review_status: draft-needs-review
links:
  repository: https://github.com/alpacahq/alpaca-postman
  architecture: ../architecture/alpaca_postman.c4
---

# Alpaca Postman Collections

## Purpose
The repository exists so that developers can start calling the public Alpaca APIs from Postman without hand-building
requests. It holds exported Postman collections for the Data, Trader and Broker APIs and points readers at the public
Postman workspace where the same collections are published (`README.md`). The README walks a newcomer through forking
the Broker collection and the sample environment, supplying their own key and secret, and sending a first Clock or
Calendar request (`README.md`).

There is no application code, build, test or deployment in the repository — only collection JSON and the README
(`git ls-files` at `ad68ba8` returns nine files). Activity has been sporadic since 2022, with the most recent commit
being a link fix in February 2024 (`git log`), so the status above is recorded as maintenance rather than active.

## Capabilities
- Broker API request set: accounts, activities, assets, calendar, clock, corporate actions, documents, events, ACH relationships, banks, transfers, journals, trading, watchlists, OAuth and rebalancing — evidence: `Postman Collections/Broker_API.json`
- Trader v2 API request set: account, orders, positions, assets, watchlists, calendar, clock, corporate action announcements, account configurations, account activities, portfolio history — evidence: `Postman Collections/Trader_v2_API.json`
- Market Data v2 request set: stock pricing, crypto pricing (v1beta1 and v1beta2) and news — evidence: `Postman Collections/Market_Data_v2_API.json`
- Archive of five superseded exports kept for reference — evidence: `Deprecated/`
- Onboarding walkthrough for forking a collection and configuring an environment — evidence: `README.md`

## Interfaces
**Inbound:** none exposed by the repository itself. The consumable surface is the collection JSON files, imported or
forked into Postman (`README.md`, `Postman Collections/`).

**Outbound:** every request in the collections targets a `{{HOST}}` environment variable — 118 occurrences in the Broker
collection, 64 in Market Data, 59 in Trader (`Postman Collections/*.json`). The Broker collection documents sandbox and
production hosts and the Trader collection documents paper and production hosts in their collection descriptions
(`Postman Collections/Broker_API.json`, `Postman Collections/Trader_v2_API.json`). All three current collections authenticate, by two different schemes: the Broker
collection uses collection-level basic auth bound to the `{{api_key}}` / `{{api_secret}}` variables
(`Postman Collections/Broker_API.json`), while the Trader v2 and Market Data v2 collections set per-request
`Apca-Api-Key-Id` and `Apca-Api-Secret-Key` headers whose values are bound to the `{{APCA_API_KEY_ID}}` and
`{{APCA_API_SECRET_KEY}}` environment variables — the hyphenated form is the HTTP header key, the underscored form is
the Postman variable the developer sets (`Postman Collections/Trader_v2_API.json`,
`Postman Collections/Market_Data_v2_API.json`).

## Dependencies
- Alpaca Broker API — the target of the Broker collection requests — evidence `Postman Collections/Broker_API.json`
- Alpaca Trading API — the target of the Trader v2 collection requests — evidence `Postman Collections/Trader_v2_API.json`
- Alpaca Market Data API — the target of the Market Data collection requests — evidence `Postman Collections/Market_Data_v2_API.json`
- Public Postman workspace — the distribution channel readers are sent to — evidence `README.md`
- Alpaca developer documentation — linked per API family — evidence `README.md`
- Alpaca account sign-up / key issuance — where the developer generates the key and secret the collections require — evidence `README.md` ("Get your API keys from here. Upon creating an account you will be prompted to generate your keys.")
- GitHub Issues on this repository — the feedback and bug-report channel named in the README — evidence `README.md` ("Issues" section)

## Data & storage
No datastores, queues or schemas. The only persisted artefacts are the eight collection JSON files
(`Postman Collections/`, `Deprecated/`). Credentials are never stored in the repository: the collections reference
`api_key` / `api_secret` variables that the developer supplies in their own environment (`README.md`,
`Postman Collections/Broker_API.json`).

## Operations
No Dockerfile, compose file, Kubernetes manifest, Terraform, serverless config or CI workflow is present
(`git ls-files` at `ad68ba8` lists only `README.md` and the eight collection JSON files). Changes reach users by
editing the exports here and through the public Postman workspace; commit subjects such as
"Postman created Trader_v2_API" indicate the current exports were last written by a Postman GitHub integration
(`git log`). That integration has not been continuous: an earlier one was added and deleted on 2021-09-29 (commits
0a3dcf1 and 614c602), hand-edits by several contributors followed through July 2022, and the commit after the
2022-08-04 re-sync is human-titled ("Christie Ruales updated Broker_API", b1a9f1d) — `git log`.

## Behaviour (Allium)
none — no `.allium` specifications exist in this repository at `ad68ba8` (`git ls-files`). Behaviour of the underlying
APIs belongs to the services the collections call, not to this repository.

## Decisions
- [ADR-0001 Publish and fork collections through a public Postman workspace](decisions/ADR-0001-publish-via-public-postman-workspace.md)
- [ADR-0002 Retire unsynced collections into a Deprecated folder](decisions/ADR-0002-deprecate-unsynced-collections.md)
- [ADR-0003 Parameterise the API host instead of hard-coding it](decisions/ADR-0003-parameterise-api-host.md)

## Evidence
- `README.md`
- `Postman Collections/Broker_API.json`
- `Postman Collections/Trader_v2_API.json`
- `Postman Collections/Market_Data_v2_API.json`
- `Deprecated/Broker API.postman_collection.json`, `Deprecated/Trader v2 API.postman_collection.json`, `Deprecated/Market Data v2 API.postman_collection.json`, `Deprecated/Data v2 stocks API.postman_collection.json`, `Deprecated/Data v2 crypto API.postman_collection.json`
- `git log` on branch `allium/layered-docs-2026-08` at `ad68ba8`

## Open questions
- Ownership is unverified: there is no CODEOWNERS file and the README names no owning team, so `owners` is left empty.
- Unverified: whether the deprecated exports are still consumed by anyone, or are kept only as history.
- Unverified: whether the exports here are regenerated automatically from the public workspace today; the commit subjects show an integration wrote them in August 2022, but nothing in the repository configures one and a previous integration was explicitly deleted in 2021 (614c602). Confidence: low.
- Unverified: whether the sign-up site and GitHub Issues are the only intake channels — the README names these two, but no support policy is recorded in the repository.
- Unverified: the sample environment referenced by the README is not in this repository, so its default host values could not be checked here.
