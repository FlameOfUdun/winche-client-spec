# Plan

## Goal

Keep every Winche client SDK (Dart today; TypeScript, Swift and Kotlin later) and the servers consistent through a
shared spec and shared tests, not shared code.

## Steps

1. **Repo setup.** The case file format, its JSON Schema, and a CI check that every case file matches it. The first
   cases are values and queries, taken from the existing Dart tests (`value_order_test`, `filter_eval`,
   `local_query_engine`) and from `DotNet/winche-database/docs/PROTOCOL.md`.
2. **Dart runner.** A dev-only test in `winche-database-dart-sdk` that fetches the cases at a pinned version and runs
   them through the SDK's own code.
3. **.NET runner.** The same cases in `winche-database`, run against the server's ordering and filter code, to prove
   the server and the clients agree.
4. **More cases and specs.**
   - Database: writes (set, update, delete, the `deleteField` sentinel, transforms), offline (local writes laid over
     server data, the order pending writes resolve in), errors (codes, HTTP status, error bodies).
   - Move the Database protocol document here from `winche-database`, which then links to it.
   - Write the Storage, Auth and Functions specs from what the Dart SDKs and servers do today, with their cases
     (storage paths, upload resume rules, error mapping).
5. **Live suite (optional).** A suite any SDK can run against `winche emulators`.

## Case areas

| Area | Covers |
| --- | --- |
| core/values | Wire encoding, ordering across types, numeric equality, NaN and -0 |
| core/paths | Document and collection paths, field paths, generated ids |
| core/errors | Error codes, HTTP status, error bodies |
| database/writes | Applying set, update, delete, `deleteField` and transforms |
| database/queries | Filter matching, `orderBy` with the tiebreaker, cursors |
| database/offline | Local writes over server data, pending write order |
| storage | Paths, metadata, upload resume |
| auth, functions | Token and session rules, call and error shapes |

## Decisions

- One repo for all products, one version.
- Specs are Markdown; cases are JSON.
- Each SDK and server pins a spec version.
- No shared code for now. A shared Rust core for the offline engine is considered only once several SDKs would each
  have to reimplement it.
