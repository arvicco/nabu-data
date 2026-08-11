# Per-document historical-stage (lect) assignments across the multilingual catalog

`mul/lect-assignments` — gold-derived tier, anchoring: document-urn. Produced by `nabu data build mul/lect-assignments` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Ancient-language corpora rarely say which historical stage of a language a text belongs to — an Akkadian tablet may be Old Babylonian or Neo-Babylonian, a Sanskrit hymn Vedic or Classical, and the difference matters to anyone studying how these languages changed. This dataset publishes Nabu's per-document stage assignments across its whole multilingual catalog: for each document (cited by its stable URN), the specific historical variety it is assigned to, plus the basis of the assignment — a period rule reading the corpus's own metadata, or an inference from the document's date — so every row says how much to trust it. No other project publishes stage assignments at corpus scale.

Publishes the per-document journal behind Nabu's lect facet — ~482K (URN, language-code) → historical-stage assignments (Old vs Neo-Babylonian, Ur III vs OB Sumerian, Vedic vs Classical Sanskrit, ...) with the basis and note in-band per row — the corpus-scale stage stratification no other project publishes; the id grammar and registry are public in nabu-lects (cited). License classes open+attribution only (nc/odbl/research_private slices excluded row-by-row, censused in nabu.eval); CC BY-SA 4.0 — the №R-24 carve-out dataset carrying the share-alike lanes (edh, aes, ...).

## Maintenance

re-derive after journal-moving events (a sync wave re-running lect rules, new owner rulings, a rebuild) — the published-slice digest makes an unchanged journal a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: lect-assignments v1: project the lect journal at URN grain, license classes open+attribution only, ordered (urn, code); published-slice sha256=efdc0cc621fae8ff61af78b35b7acef3101fa60422b351ae57e27d0efacb2b40

Derivation fingerprint: `ef4a1e07fbb6f82d2eb7d31f4aa5e9b34ef4c145bb7b5851e62744d15532b175`.
