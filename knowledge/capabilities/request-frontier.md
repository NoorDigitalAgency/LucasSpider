---
schema_version: 1
kind: capability
id: lucasspider-request-frontier
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:38.994890+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/Builder.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/BloomFilter.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/HashAlgorithmService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/IHashAlgorithmService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/IRequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/MD5HashAlgorithmService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/MurmurHashAlgorithmService.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestHasher.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/RequestedQueue.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/BloomFilterOptions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/FakeDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/HashSetDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/Component/IDuplicateRemover.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/IScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueBfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/SchedulerBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/ServiceCollectionExtensions.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Spider.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Http/Request.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Scheduling, hashing, deduplication and pending timeouts

AddRequestsAsync accepts strings, arrays or an enumerable. String input receives configured timeout/UserAgent; object input retains its supplied values. Owner is overwritten with this spider’s ID after retry/depth/downloader checks. SchedulerBase recomputes the hash, invokes the chosen duplicate remover, pushes nonduplicates and returns the admitted count; total is supplied by that remover. SuccessAsync and FailAsync are no-op hooks in this base. [src/LucasSpider/Spider.cs:L166–L230](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L166-L230), [src/LucasSpider/Scheduler/SchedulerBase.cs:L1–L129](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/SchedulerBase.cs#L1-L129).

RequestHasher serializes Owner, absolute URI, Method, RequestedTimes and Content before applying the injected hash algorithm and Base64 representation. Thus equal URLs are not necessarily equal work, retries can acquire different hashes, and headers/depth/properties are not fields of this hash projection. The host registers MurmurHashAlgorithmService by default; an owned builder extension selects MD5 or a custom request hasher. This correlation/deduplication representation does not authenticate a request. [src/LucasSpider/Infrastructure/RequestHasher.cs:L1–L33](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestHasher.cs#L1-L33), [src/LucasSpider/Builder.cs:L163–L170](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Builder.cs#L163-L170), [src/LucasSpider/ServiceCollectionExtensions.cs:L15–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/ServiceCollectionExtensions.cs#L15-L37), [src/LucasSpider/Infrastructure/HashAlgorithmService.cs:L1–L32](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/HashAlgorithmService.cs#L1-L32), [src/LucasSpider/Infrastructure/MurmurHashAlgorithmService.cs:L1–L20](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/MurmurHashAlgorithmService.cs#L1-L20), [src/LucasSpider/Infrastructure/MD5HashAlgorithmService.cs:L1–L19](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/MD5HashAlgorithmService.cs#L1-L19).

The BFS list implementations take/remove from the front and return cloned requests; distinct variants use an injected remover, while nondistinct constructors use FakeDuplicateRemover. Distinct DFS takes the tail in reverse order. The nondistinct QueueDfsScheduler has a different start expression: its inclusive loop can select one extra item when the requested count is met, and at equality can index below the list; removal still uses dequeueCount. It must not be documented as equivalent to the distinct DFS implementation or as a verified correct DFS policy. [src/LucasSpider/Scheduler/QueueBfsScheduler.cs:L1–L63](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueBfsScheduler.cs#L1-L63), [src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs:L1–L60](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs#L1-L60), [src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/QueueDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs:L1–L35](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/ServiceCollectionExtensions.cs#L1-L35).

HashSetDuplicateRemover validates nonempty Owner and equality to its initialized spider ID, stores hashes in a concurrent in-memory dictionary, and supports whole-set or per-request reset. That equality is a routing invariant, not tenant authorization. FakeDuplicateRemover counts calls and returns false. BloomFilterDuplicateRemover uses configurable probabilistic membership, counts newly observed entries and can clear/recreate its filter; per-request reset throws NotImplementedException. Its counter reset assigns the old value returned by Interlocked.Exchange back to the field, leaving the prior count unchanged absent a concurrent increment. Enabling completed-request resets with this remover can therefore throw. [src/LucasSpider/Scheduler/Component/HashSetDuplicateRemover.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/Component/HashSetDuplicateRemover.cs#L1-L79), [src/LucasSpider/Scheduler/Component/FakeDuplicateRemover.cs:L1–L49](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/Component/FakeDuplicateRemover.cs#L1-L49), [src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/Component/BloomFilterDuplicateRemover.cs#L1-L78), [src/LucasSpider/Scheduler/Component/BloomFilterOptions.cs:L1–L8](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/Component/BloomFilterOptions.cs#L1-L8), [src/LucasSpider/Infrastructure/BloomFilter.cs:L1–L481](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/BloomFilter.cs#L1-L481).

RequestedQueue rejects any request timeout below 2,000 ms at dispatch, including a caller-set Request.Timeout that bypassed constructor DefaultTimeout validation. The throw propagates from publishing through RunAsync's catch/finally and ends the crawl, rather than rejecting only that request. It adds admitted work by hash, and schedules a hashed-wheel callback carrying the original timestamp. Dequeue removes by hash; a stale callback cannot remove a newer timestamp for that hash. Collected timeouts are copied and the bag exchanged/cleared; disposal clears dictionaries/bags and stops the timer. This is process memory, separate from the scheduler frontier and duplicate history, and no crash recovery is implemented here. [src/LucasSpider/Infrastructure/RequestedQueue.cs:L1–L118](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/RequestedQueue.cs#L1-L118).

Related: [lifecycle](crawl-lifecycle.md), [model cloning](../systems/request-response-models.md) and [follow-request construction](response-data-flow.md). Scheduling concurrency, probabilistic false positives, list edge cases and deployment binding require review; source inspection did not run these paths.

The owned queue scheduler enqueue methods store the admitted Request reference; cloning occurs during dequeue. Consequently an admitted data-flow retry can still share the context request when finally disposes it, clearing headers/properties and disposing binary content before a later clone. Duplicate rejection or earlier dequeue changes that branch. See the complete [retry cleanup contract](response-data-flow.md). [src/LucasSpider/Scheduler/QueueBfsScheduler.cs:L1–L63](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueBfsScheduler.cs#L1-L63), [src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs:L1–L60](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctBfsScheduler.cs#L1-L60), [src/LucasSpider/Scheduler/QueueDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDfsScheduler.cs#L1-L78), [src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs:L1–L78](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Scheduler/QueueDistinctDfsScheduler.cs#L1-L78), [src/LucasSpider/Spider.cs:L363–L405](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Spider.cs#L363-L405), [src/LucasSpider/Http/Request.cs:L291–L304](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Http/Request.cs#L291-L304).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
