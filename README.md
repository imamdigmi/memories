# Memory backups
`hindsight/_raw/hindsight_full.sql.gz` = pg_dump of the whole Hindsight DB (all banks, embeddings, graph).
Restore: `gunzip -c hindsight_full.sql.gz | psql -h 127.0.0.1 -U hindsight -d hindsight`
History is squashed to one commit per run to keep the repo small.
