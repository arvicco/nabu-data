# The cross-dictionary reference graph — every machine-marked entry→entry pointer

`mul/dictionary-crossrefs` — gold-derived tier, anchoring: entry-urn. Produced by `nabu data build mul/dictionary-crossrefs` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Which dictionary entries point at which? Historical dictionaries are dense with cross-references — LSJ's "v. μῦθος", JMdict's antonyms, the Hebrew lexical index's pointers into BDB, the AED's root links, Wiktionary's reconstructed-etymon synonyms — but the pointers have only ever been readable inside each dictionary's own markup. This dataset publishes Nabu's cross-reference estate as one queryable graph: every machine-marked pointer of the open dictionaries, its kind and verbatim label, and where the target headword resolves unambiguously, the target entry by stable URN — across Greek, Latin, Japanese, Chinese, Hebrew, Egyptian and the reconstructed proto-languages.

The cross-reference estate of Nabu's dictionaries as one queryable graph — no one publishes cross-dictionary link data for these languages. One row per edge: the from-entry (dictionary, stable entry URN, headword), the pointer's kind and verbatim label, the target as the dictionary stores it (display form, folded form, upstream id), and where the target resolved unambiguously the target dictionary and entry URN; an unresolved edge is still an edge and publishes with the target-entry fields empty (both resolution states censused). License screening on BOTH endpoints: an edge publishes only when its own dictionary's source is open/attribution class AND, when resolved, the target entry's dictionary's source is too — an nc endpoint on either side drops the edge, censused per endpoint role and class in nabu.eval; CC BY-SA 4.0 — the share-alike carve-out carrying the share-alike dictionaries (Wiktionary, JMdict, LSJ, AED, ...).

## Maintenance

re-derive after dictionary-source syncs or a rebuild (the loader's resolution pass re-mints the graph); the published-slice digest makes an unchanged graph a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: dictionary-crossrefs v1: project dictionary_crossrefs one row per edge of a live entry, entries referenced by catalog URN, resolved targets joined by to_entry_id, license classes open+attribution only on BOTH endpoints (source dictionary always, target dictionary when resolved), ordered (dictionary, entry URN, seq); published-slice sha256=e38594a3ecfe7f8347e4015a5213114dd7a339168b5066e8e91026a558de5e35

Derivation fingerprint: `56393a692b0a97a2f0878502a4488fc14a3c7af9743ede95a35322d8160b8dae`.
