---
type: Architecture Decision
title: ADR-0001 Publish and fork collections through a public Postman workspace
description: Collections are distributed from a public Postman workspace and consumed by forking, with this repository holding the exported JSON.
status: accepted
date: 2022-08-04
deciders: []
supersedes: []
affects: [alpaca_postman, alpaca_postman.broker_collection, alpaca_postman.trader_collection, alpaca_postman.market_data_collection, ext_postman_workspace]
allium: []
evidence: ["README.md", "Postman Collections/Broker_API.json", "commit 0a3dcf1 Postman created Broker API.postman_collection.json", "commit 614c602 Delete postman integration", "commit 411ab7b Postman created Broker_API", "commit acc4577 Postman created Trader_v2_API", "commit 99299ea Postman created Market_Data_v2_API", "commit b1a9f1d Christie Ruales updated Broker_API"]
tags: [alpacahq, adr, generated]
timestamp: 2026-08-21T21:43:34Z
generated_by: claude-opus-5 / layered-docs 2026-08
source_commit: ad68ba8e7a79725108f8df68cc4a12e9f01d6a75
source_branch: allium/layered-docs-2026-08
generated_at: 2026-08-21T21:43:34Z
confidence: low
review_status: draft-needs-review
---

# ADR-0001 Publish and fork collections through a public Postman workspace

## Context
Developers evaluating the public APIs need runnable example requests, and those examples have to stay current as the
APIs change. The repository README opens by pointing readers at a public Postman workspace rather than at the files in
the repository, and the whole "Getting Started" walkthrough is expressed in Postman fork operations — fork the
collection, fork the sample environment, select the environment, send the Clock request (`README.md`).

The arrangement has not been stable. A Postman GitHub integration first wrote a collection on 2021-09-29 (commit
0a3dcf1 "Postman created Broker API.postman_collection.json") and was removed the same day by commit 614c602
("Delete postman integration"). The collections were then hand-maintained through July 2022 by several contributors
(commits "Adding v1beta2 endpoints", "Update Broker API.postman_collection.json", "Add Assets and Corporate Actions"),
and were re-synced from the workspace on 2022-08-04. The commit immediately following the Broker re-sync is
human-titled (b1a9f1d, 2022-08-08, "Christie Ruales updated Broker_API") — `git log`.

## Decision
Collections are published in the public Postman workspace and consumed by forking there; this repository
holds the exported JSON as a mirror and an issue-reporting surface.

> Unverified: the three current exports were *last* written by the Postman GitHub integration, as the commit subjects
> "Postman created Broker_API", "Postman created Trader_v2_API" and "Postman created Market_Data_v2_API" show
> (`git log`). That the workspace is a standing source of record cannot be evidenced: nothing in the repository
> configures an integration, an earlier integration was deleted days after being added (614c602), and hand-edits
> continued afterwards. Confidence: low.

## Consequences
- The repository has no build, test or deployment machinery; nine files at `ad68ba8` are the README and eight collection JSON exports (`git ls-files`).
- Users supply their own key and secret in a forked environment, so no credentials sit in the repository; the collections reference `api_key` / `api_secret` variables instead (`Postman Collections/Broker_API.json`).
- Feedback is routed to GitHub issues even though the artefacts are edited in Postman (`README.md`, "Issues" section).
- Drift between the workspace and the mirrored exports is possible and is not detected by anything in the repository.

## Alternatives considered
Not recorded in the repository.
