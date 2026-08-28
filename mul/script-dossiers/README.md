# Curated script dossiers — the human-written context per writing system

`mul/script-dossiers` — curated tier, anchoring: script-tag. Produced by `nabu data build mul/script-dossiers` (Nabu 1.5.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

## Why this dataset exists — in plain terms

What is this writing system, and how does a working research library actually hold it? One curated dossier per script in the registry's global scripts table — a human-written context paragraph (what the script is, when and how it ran) and, where it applies, the desk conventions the originating library uses (transliteration surfaces, fold tables, honest gaps). Each row is one attribute of one script, keyed by its lowercased ISO 15924 tag. Own authorship throughout (CC BY 4.0); the source of truth is the library's config/script_dossiers.yml, of which this dataset is the public mirror.

The char desk's script layer (P86, №R-49): every writing system in the registry's scripts table gets a human-written dossier — what the script IS, and the desk conventions a working library actually uses for it (transliteration surfaces, fold tables, honest gaps). Unlike the language dossiers (curated per-instance in local/), the source of truth is the git-shared config fact file, so every install answers identically and this dataset is the citable public mirror. The suite's drift guard pins dossier tags to the nabu-lects scripts table, so registry mints and dossiers cannot diverge silently.

## Maintenance

re-derive after editing config/script_dossiers.yml (a new registry script mint forces a dossier via the drift guard); the published-slice digest makes an unchanged table a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: script-dossiers v1: publish the curated per-script dossiers (name, context, desk conventions) from config/script_dossiers.yml, one tidy row per (tag, attribute), tag order; the registry drift guard pins tags == the nabu-lects scripts table; published-slice sha256=9d1b304ec60d38fb16565685529e7283a77b6fa3cf57a80533e75898d641d981

Derivation fingerprint: `9fcc1df416105ba9e4db5d5f774382ad25757b4d0907ae04d3cda2cb167653ef`.
