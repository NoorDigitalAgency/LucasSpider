---
schema_version: 1
kind: system
id: lucasspider-entity-storage
project_id: lucasspider
owner: zlzforever, Sojaner
status: proposed
classification: sensitive-metadata
source_commit: 495ed7cc49208acaa50de7dcf5ebdec584394000
last_verified: 2026-10-14T11:13:39.486177+00:00
expiry_policy: until-overridden-or-removed
evidence:
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/Column.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/ConsoleEntityStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityFileStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/EntityStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/IndexMetadata.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/Schema.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/SqlStatements.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/StorageMode.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/TableMetadata.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/DataFlow/Storage/TablePostfix.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
- repository: lucasspider
  path: src/LucasSpider/Infrastructure/DateTimeHelper.cs
  revision: 495ed7cc49208acaa50de7dcf5ebdec584394000
conflicts: []
---

# Entity metadata, files and relational writes

EntityStorageBase accepts only data keyed by a CLR Type implementing IEntity, collects valid entity objects from a value or enumerable, and invokes the concrete storage. EntityBase reflects readable/writable properties into Column metadata, derives schema/table names, Required/StringLength flags, keys, indexes and update columns; expression helpers support member/new/conversion shapes and reject others. It uses a Lazy TableMetadata but repopulates its Columns with Add on every metadata request, so repeated calls on the same entity can encounter duplicate keys. TableMetadata infers auto-increment only from its supported single-primary type cases. [src/LucasSpider/DataFlow/Storage/EntityStorageBase.cs:L1–L73](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityStorageBase.cs#L1-L73), [src/LucasSpider/DataFlow/Storage/EntityBase.cs:L1–L186](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityBase.cs#L1-L186), [src/LucasSpider/DataFlow/Storage/TableMetadata.cs:L1–L79](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/TableMetadata.cs#L1-L79), [src/LucasSpider/DataFlow/Storage/Column.cs:L1–L20](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/Column.cs#L1-L20), [src/LucasSpider/DataFlow/Storage/Schema.cs:L1–L38](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/Schema.cs#L1-L38), [src/LucasSpider/DataFlow/Storage/IndexMetadata.cs:L1–L45](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/IndexMetadata.cs#L1-L45).

Entity file storage caches metadata by CLR Type and derives files under an owner folder with schema/table-derived names. JsonEntityFileStorage caches StreamWriter by TypeName, writes serialized entity batches as lines and disposes writers on shutdown; the writer key omits Owner, so an instance reused across owners can retain the first opened owner path for a type. File.OpenWrite is used rather than an append/atomic transaction contract. ConsoleEntityStorage prints grouped entities. Output permissions, identifier/path constraints and retention are unknown. [src/LucasSpider/DataFlow/Storage/EntityFileStorageBase.cs:L1–L97](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityFileStorageBase.cs#L1-L97), [src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs:L1–L53](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/JsonEntityFileStorage.cs#L1-L53), [src/LucasSpider/DataFlow/Storage/ConsoleEntityStorage.cs:L1–L35](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/ConsoleEntityStorage.cs#L1-L35).

Relational storage requires a nonblank connection string, retries connection creation/open up to RetryTimes, caches metadata and generated SQL, and runs database/table creation before per-batch writes. DDL caching uses the table-creation SQL as key and opens a separate connection in that callback without a using scope there. Mode selects insert, insert-ignore, update or insert-and-update; UseTransaction optionally begins/commits a transaction. Caught write errors are logged; only an InnerException of EndOfStreamException reaches another loop attempt, while other exceptions attempt rollback and break without rethrowing. Thus an awaited storage call need not mean all writes succeeded, and exhausted retries are not surfaced by this branch. [src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs:L1–L278](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs#L1-L278), [src/LucasSpider/DataFlow/Storage/StorageMode.cs:L1–L28](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/StorageMode.cs#L1-L28), [src/LucasSpider/DataFlow/Storage/SqlStatements.cs:L1–L43](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlStatements.cs#L1-L43).

SqlServerOptions parses configured enum/int/bool inputs and supplies source defaults; CreateFromOptions builds SqlServerEntityStorage and copies retry/transaction/case settings. The concrete provider is Microsoft.Data.SqlClient and command execution uses Dapper. Generated insert-ignore SQL is assigned from the same GenerateInsertSql as ordinary insert, so the mode name does not prove duplicate suppression. Updates require generated update columns/keys; insert-and-update generation returns no statement when there is no primary key. SQL identifiers come from metadata and are interpolated into generated commands; data values use parameter placeholders. Provider/collation/DDL permissions/schema compatibility and atomicity beyond optional local transactions remain unverified. [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L26–L133](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L26-L133), [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L247–L343](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L247-L343), [src/LucasSpider/DataFlow/Storage/TablePostfix.cs:L1–L28](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/TablePostfix.cs#L1-L28).

The base computes date-postfixed table names/cache keys, but the concrete SQL generators read Schema.Table directly; a date postfix does not establish that the emitted table name changes. Static source is authoritative for these distinctions, not generated SQL previews or sanitized string placeholders. No database, connection, credentials, schema or customer data were opened. Related: [ordinary storage](../capabilities/response-data-flow.md) and [entity extraction](../capabilities/entity-extraction.md).

Column.Type is the reflected PropertyType.Name. The concrete SQL type switch maps Boolean to bit, DateTime and DateTimeOffset to datetime with a GETDATE() default, Decimal to decimal(18,2), Double and Single to float, Int32 and Byte to int, and Int64 to bigint. Other type names use the string branch: length at or below zero or above 8000 gives NVARCHAR(MAX), otherwise VARCHAR(length). Column.Length defaults to 255 and StringLength.MaximumLength can override it. The declared ShortType constant has no switch case; CLR Int16, Guid and nullable/other unmatched names therefore reach the string branch. Primary or Required columns receive NOT NULL; other columns do not receive that clause from this generator. These are owned SQL-generation contracts, not an inspected database schema or provider conversion guarantee. [src/LucasSpider/DataFlow/Storage/EntityBase.cs:L27–L96](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/EntityBase.cs#L27-L96), [src/LucasSpider/DataFlow/Storage/Column.cs:L1–L20](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/Column.cs#L1-L20), [src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs:L28–L37](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs#L28-L37), [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L350–L426](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L350-L426).

Missing SqlServerOptions.ServerVersion configuration selects V2008, whereas the direct SqlServerEntityStorage constructor defaults to V2017. The relational base initializes IgnoreCase true, but missing configured IgnoreCase becomes false and CreateFromOptions overwrites the base value with it; true lowercases generated names and does not establish database collation behavior. RetryTimes defaults to 600; UseTransaction is false unless enabled. Connection-string input is required, with its value withheld. DateTimeHelper.Monday supplies the base Monday postfix calculation (Sunday minus six days, otherwise plus one), but the concrete generators still use Schema.Table rather than the base postfixed name. [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L1–L105](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L1-L105), [src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs:L26–L133](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/SqlServerEntityStorage.cs#L26-L133), [src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs:L81–L166](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/DataFlow/Storage/RelationalDatabaseEntityStorageBase.cs#L81-L166), [src/LucasSpider/Infrastructure/DateTimeHelper.cs:L42–L84](https://github.com/NoorDigitalAgency/LucasSpider/blob/495ed7cc49208acaa50de7dcf5ebdec584394000/src/LucasSpider/Infrastructure/DateTimeHelper.cs#L42-L84).

Confidence: high for the cited pinned owned source; external/runtime/authority boundaries are explicitly unknown. Freshness: revalidate affected source and consumed pins when changed. Proposed status is not human acceptance.
