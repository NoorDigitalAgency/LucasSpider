# LucasSpider repository knowledge

Start with [project and workflow navigation](project.md). All 18 records remain proposed at source `495ed7cc49208acaa50de7dcf5ebdec584394000`. Complete native production source is the authority; screened graph structure is navigation only. Historical attribution: zlzforever and Sojaner; current accepting steward is unknown and no reviewer is currently requested.

- [LucasSpider: crawl host, frontier, workers and extraction](project.md) — `lucasspider-project`.
- [Dispatch, retries, completion and shutdown](capabilities/crawl-lifecycle.md) — `lucasspider-crawl-lifecycle`.
- [Scheduling, hashing, deduplication and pending timeouts](capabilities/request-frontier.md) — `lucasspider-request-frontier`.
- [HTTP conversion, redirects and failure responses](capabilities/http-download.md) — `lucasspider-http-download`.
- [Browser rendering, file/fake downloaders and PPPoE](capabilities/browser-file-download.md) — `lucasspider-browser-file-download`.
- [Ordered response processing and ordinary output storage](capabilities/response-data-flow.md) — `lucasspider-response-data-flow`.
- [Attribute-driven entity extraction and conversion](capabilities/entity-extraction.md) — `lucasspider-entity-extraction`.
- [Selectable adapters, selector caches and formatter contracts](systems/selectors-and-formatters.md) — `lucasspider-selectors-and-formatters`.
- [Entity metadata, files and relational writes](systems/entity-storage.md) — `lucasspider-entity-storage`.
- [Proxy supply, validation, leasing and handler feedback](systems/proxy-rotation.md) — `lucasspider-proxy-rotation`.
- [Transport, serialization, routing and consumer lifecycle](systems/message-queue.md) — `lucasspider-message-queue`.
- [Agent registration, heartbeat, counters and local stores](systems/agents-and-statistics.md) — `lucasspider-agents-and-statistics`.
- [Request/response values, headers, cloning and utility boundaries](systems/request-response-models.md) — `lucasspider-request-response-models`.
- [Host configuration, service resolution and disposal](systems/host-composition.md) — `lucasspider-host-composition`.
- [Declared targets, dependencies, CI and publication boundaries](systems/build-package-boundaries.md) — `lucasspider-build-package-boundaries`.
- [Crawl terms and source-local representations](vocabulary/crawl-terms.md) — `lucasspider-crawl-terms`.
- [Historical attribution, acceptance and synchronization](governance/ownership.md) — `lucasspider-ownership`.
- [Source edge cases, unknown deployments and policy questions](decisions/conflicts-and-open-questions.md) — `lucasspider-open-questions`.

The complete source/operation/directory matrices, original-body continuity, privacy/native proofs and ten-section interview report are frozen outside this checkout under the Avalon handoff target. Independent full semantic, omission, coherence and readability review precedes publication. Preserve all IDs/history and current PR 52 / issue 35. Source, dependency, configuration or workflow changes require affected-record revalidation until overridden or removed. Merge, human acceptance and accepted-only indexing are separate authorized steps.

Validation from Avalon: `out/rerun/lynx-api/venv/bin/python scripts/kb-simulation/validate.py out/rerun/repos/noordigitalagency/lucasspider --source lucasspider=out/rerun/repos/noordigitalagency/lucasspider`. Validation checks schema/evidence/link/freshness, not application runtime.
