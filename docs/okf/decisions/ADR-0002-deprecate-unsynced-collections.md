---
type: Architecture Decision
title: ADR-0002 Retire unsynced collections into a Deprecated folder
description: Superseded collection exports are moved into a Deprecated folder rather than deleted; established in January 2022 for the Data v2 collections and applied again in August 2022 to the collections replaced by the synced exports.
status: accepted
date: 2022-01-26
deciders: []
supersedes: []
affects: [alpaca_postman, alpaca_postman.deprecated_collections]
allium: []
evidence: ["commit 936819f Move old data collections to deprecated", "commit 792974c Move unsynced collections to Deprecacted folder", "Deprecated/", "Postman Collections/"]
tags: [alpacahq, adr, generated]
timestamp: 2026-08-21T21:43:34Z
generated_by: claude-opus-5 / layered-docs 2026-08
source_commit: ad68ba8e7a79725108f8df68cc4a12e9f01d6a75
source_branch: allium/layered-docs-2026-08
generated_at: 2026-08-21T21:43:34Z
confidence: medium
review_status: draft-needs-review
---

# ADR-0002 Retire unsynced collections into a Deprecated folder

## Context
The repository carried hand-edited `*.postman_collection.json` files that contributors updated directly (commits such as
"Adding v1beta2 endpoints", "Add Assets and Corporate Actions", "Update Broker API.postman_collection.json" — `git log`).
The archive-rather-than-delete pattern was established on 2022-01-26 by commit 936819f ("Move old data collections to
deprecated"), which created the `Deprecated/` folder with `Data v2 crypto API.postman_collection.json` and
`Data v2 stocks API.postman_collection.json` (`git log --diff-filter=A -- 'Deprecated/*'`, `git show --stat 936819f`).
The same pattern was applied again on 2022-08-08 by commit 792974c ("Move unsynced collections to Deprecacted folder"),
which added the Broker, Market Data v2 and Trader v2 exports superseded by the synced exports that had landed under
`Postman Collections/` four days earlier (`git show --stat 792974c`, `git log`).

## Decision
Collections that are superseded — first the older Data v2 exports, later those replaced by the workspace-synced
exports — are moved into `Deprecated/` and kept, rather than deleted, so history and any still-linked file remain
reachable. The five archived exports are Broker, Trader v2, Market Data v2, Data v2 stocks and Data v2 crypto
(`Deprecated/`).

## Consequences
- Two exports of the same collection now coexist: `Deprecated/` uses Postman collection schema v2.1.0 while `Postman Collections/` uses v2.0.0, and the deprecated Broker export carries 36 request URLs against 43 in the current one (`Deprecated/Broker API.postman_collection.json`, `Postman Collections/Broker_API.json`).
- Two crypto and stocks data collections have no successor under `Postman Collections/`; their endpoints appear consolidated into the single Market Data v2 export (`Deprecated/Data v2 crypto API.postman_collection.json`, `Deprecated/Data v2 stocks API.postman_collection.json`, `Postman Collections/Market_Data_v2_API.json`).
- Readers can pick the wrong file, since nothing in the README distinguishes the two folders (`README.md`).
- The later move commit misspells the folder in its subject ("Deprecacted") while the folder itself and the creating commit 936819f spell it correctly, so searching history by commit subject alone can miss that move (`git log`, commits 936819f and 792974c).

## Alternatives considered
Not recorded in the repository.

## Open questions
- Unverified: whether the two 2022-01-26 Data v2 moves and the 2022-08-08 move reflect one standing policy or two separate ad-hoc decisions; no written policy exists in the repository, so this ADR records the observed pattern only.
