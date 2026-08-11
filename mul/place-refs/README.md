# Per-document place references across the multilingual catalog, gazetteer-ready

`mul/place-refs` — gold-derived tier, anchoring: document-urn. Produced by `nabu data build mul/place-refs` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Ancient documents name the places they were written in or found at, but every corpus records that differently — a verbatim findspot string, a gazetteer URL, sometimes several. This dataset publishes Nabu's compiled projection across its whole multilingual catalog: for each document (cited by its stable URN), each place it references as a clean namespaced identifier (pleiades:, tm:, geonames:, cigs:, np:) ready to join against the public gazetteers, alongside the verbatim name the corpus used and the basis of the link — asserted by the upstream corpus itself, or applied from the nabu-places curation registry. Mapping and GIS pipelines can join texts to gazetteer geometry without re-solving each corpus's ref spelling.

Publishes the compiled doc→place projection behind Nabu's places desk — ~586K (URN, claim) rows, every historical ref spelling (verbatim upstream URLs, multi-URL fields, namespaced mints) folded to clean namespace:id form (pleiades:, tm:, geonames:, cigs:, np:) ready to join gazetteer geometry, with the verbatim upstream name and the Basis (upstream-asserted vs nabu-places-applied) in-band per row. License classes open+attribution only (the iip nc slice excluded row-by-row, censused in nabu.eval); CC BY-SA 4.0 — the №R-24 carve-out (edh/aes/elephantine/ceipom share-alike lanes and the conservative tm:-index inheritance ride inside it).

## Maintenance

re-derive after place-moving events (a sync wave, a nabu-places registry sync + apply, a rebuild) — the published-slice digest makes an unchanged projection a fingerprint no-op

## Provenance

Canonical inputs at derivation:

- `nabu-places` @ `b196b9a41270ab7831383e3a853d35391fc712ab`

Recipe: place-refs v1: project document_axes.place_ref through Nabu::PlaceRefs at (document, claim) grain, license classes open+attribution only, ordered (urn, axis row), sharded ≤250000 rows/file (№R-29); published-slice sha256=b4d2a9e76455a0ef26661d8fffc06d2f295c36d633eb58aa7ba76c8b1d308b51

Derivation fingerprint: `17ed9a0cf18e17a4ab0ca2a40f915a5a362907e33e14bb561b8799f419d9d607`.
