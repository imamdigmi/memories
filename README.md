# Memory backups

One top-level folder per memory *provider* (currently only `hindsight`; a future
second engine, e.g. mem0 or Zep, gets its own sibling folder here).

## hindsight/
- `_raw/hindsight_full.sql.gz` — authoritative `pg_dump` of the whole Hindsight
  Postgres DB (all banks, full fidelity incl. vector embeddings and the entity
  graph). This is the real disaster-recovery artifact: restore with
  `gunzip -c hindsight_full.sql.gz | psql -h HOST -U hindsight -d hindsight`.
- `banks/<bank_id>/` — one folder per memory bank, human-readable + diffable
  JSON/JSONL export via the `hindsight` CLI (facts, documents, entities,
  mental models, directives). Useful for audit/grep/portability even without
  Postgres, but **does not include embeddings** — restoring from this alone
  means Hindsight has to recompute them (costs API calls, may drift slightly).

Restore priority: use `_raw/*.sql.gz` for a real disaster-recovery restore;
use `banks/` to read/search/audit what's in memory without spinning up Hindsight.
