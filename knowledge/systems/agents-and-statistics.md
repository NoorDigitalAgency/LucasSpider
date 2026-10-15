---
schema_version: 1
kind: system
id: lucasspider-agents-and-statistics
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: '2026-10-14T02:05:11.715079+00:00'
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/AgentService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Agent/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/AgentCenterOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/AgentCenterService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/Store/AgentHeartbeat.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/Store/AgentInfo.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/Store/IAgentStore.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/AgentCenter/Store/InMemoryAgentStore.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/MachineInfo.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/IStatisticsClient.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/StatisticsClient.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/StatisticsService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/Store/AgentStatistics.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/Store/DefaultStatisticsStore.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/Store/IStatisticsStore.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Statistics/Store/SpiderStatistics.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Agent registration, heartbeat, counters and local stores

AddAgent registers its injected downloader and AgentService, HTTP client services and an empty proxy sentinel if none exists. The agent constructor stores the downloader name as the host’s default. ExecuteAsync registers statistics, optionally publishes distributed agent registration with machine information, consumes downloader work and optionally adds an agent route plus periodic heartbeats. A matching exit ID stops the application; download tasks are started separately and are not explicitly joined at StopAsync, which closes its consumers and awaits the base stop. [src/LucasSpider/Agent/ServiceCollectionExtensions.cs:L1–L28](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/ServiceCollectionExtensions.cs#L1-L28), [src/LucasSpider/Agent/AgentOptions.cs:L1–L15](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentOptions.cs#L1-L15), [src/LucasSpider/Agent/AgentService.cs:L1–L231](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L1-L231).

AgentCenterService determines its local/distributed logging branch by the concrete queue type, ensures the selected IAgentStore, then deserializes register/heartbeat messages and forwards AgentInfo/AgentHeartbeat. Decode errors are caught; outer startup/consume errors are logged. The owned InMemoryAgentStore calls TryAdd for registrations, snapshots current values, and on heartbeat only refreshes a known AgentInfo timestamp; it does not persist heartbeat resource metrics. AgentInfo.Online compares age to its source threshold. This is worker presence metadata, not an authenticated membership or current availability proof. [src/LucasSpider/AgentCenter/AgentCenterService.cs:L1–L110](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/AgentCenterService.cs#L1-L110), [src/LucasSpider/AgentCenter/ServiceCollectionExtensions.cs:L1–L16](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/ServiceCollectionExtensions.cs#L1-L16), [src/LucasSpider/AgentCenter/Store/InMemoryAgentStore.cs:L1–L38](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/Store/InMemoryAgentStore.cs#L1-L38), [src/LucasSpider/AgentCenter/Store/AgentInfo.cs:L1–L83](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/Store/AgentInfo.cs#L1-L83), [src/LucasSpider/AgentCenter/Store/AgentHeartbeat.cs:L1–L65](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/Store/AgentHeartbeat.cs#L1-L65), [src/LucasSpider/AgentCenter/Store/IAgentStore.cs:L1–L34](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/AgentCenter/Store/IAgentStore.cs#L1-L34).

StatisticsClient serializes start/exit/total/success/failure, agent registration/timing and print commands. StatisticsService initializes the selected store and forwards each recognized DTO in its callback; it catches handler errors, and unknown messages are serialized for logging. Spider accounts agent time using response.Elapsed.Milliseconds, the component rather than TotalMilliseconds, so it is not a reliable whole-duration measurement by construction. Agent heartbeat CpuLoad is a constant in this path, despite an available separate CPU sampling utility. [src/LucasSpider/Statistics/StatisticsClient.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/StatisticsClient.cs#L1-L79), [src/LucasSpider/Statistics/StatisticsService.cs:L1–L122](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/StatisticsService.cs#L1-L122), [src/LucasSpider/Spider.cs:L308–L347](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L308-L347), [src/LucasSpider/Agent/AgentService.cs:L181–L193](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L181-L193).

DefaultStatisticsStore protects a dynamic dictionary with a static lock, creates mutable spider/agent statistics by ID, increments counts/timing and updates start/exit/name/timestamp fields. Returned objects are shared, and both paged query methods throw NotImplementedException. Spider and agent entries share the same key dictionary, so incompatible type reuse is not prevented by separate namespaces here. IncreaseElapsedMilliseconds converts its signed input to uint before adding. These counters measure selected calls, not unique successful crawls, accounting/billing, durable records or a database-backed metrics service. [src/LucasSpider/Statistics/Store/DefaultStatisticsStore.cs:L1–L173](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/Store/DefaultStatisticsStore.cs#L1-L173), [src/LucasSpider/Statistics/Store/SpiderStatistics.cs:L1–L109](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/Store/SpiderStatistics.cs#L1-L109), [src/LucasSpider/Statistics/Store/AgentStatistics.cs:L1–L81](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/Store/AgentStatistics.cs#L1-L81), [src/LucasSpider/Statistics/ServiceCollectionExtensions.cs:L1–L17](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Statistics/ServiceCollectionExtensions.cs#L1-L17).

MachineInfo selects platform-specific memory readers and catches failure by returning default; callers access Current.Memory/AvailableMemory without a null guard in the agent path. The separate CPU helper samples process CPU across a delay. Platform ABI/filesystem access is a runtime boundary, and default results must not be promoted to verified machine capacity or telemetry availability. [src/LucasSpider/Infrastructure/MachineInfo.cs:L1–L321](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/MachineInfo.cs#L1-L321), [src/LucasSpider/Agent/AgentService.cs:L65–L74](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L65-L74), [src/LucasSpider/Agent/AgentService.cs:L181–L193](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Agent/AgentService.cs#L181-L193).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
