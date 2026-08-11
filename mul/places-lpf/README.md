# Referenced places as Linked Places Format v1.3 + LP-TSV (the gazetteer-exchange shape)

`mul/places-lpf` — gold-derived tier, anchoring: none. Produced by `nabu data build mul/places-lpf` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Every place the documents of Nabu's catalog reference, published in the format the digital-gazetteer world exchanges: Linked Places Format (LPF) GeoJSON plus the LP-TSV table the World Historical Gazetteer accepts as an upload. Each place carries the spellings ancient documents actually attest (cited to their corpora), coordinates and a title where the underlying gazetteers record them, the span of years the referencing documents date to, and cross-gazetteer closeMatch links — so a historical-GIS project can put these corpora on a map without re-solving any of it.

Publishes every place the catalog's documents reference as an LPF v1.3 FeatureCollection plus the LP-TSV v0.5 upload table (the World Historical Gazetteer's intake shapes): one Feature per claim (merging identities is entity resolution — the crosswalk rides as closeMatch links instead), attested spellings cited to their corpora, titles/coordinates from place_index (never invented), when-spans aggregated from document dates. The P69-2 GeoNames rider resolved NOT WANTED (recorded in the builder): geonames claims publish at document grain in mul/place-refs. CC BY-SA 4.0 — the TM lane's share-alike inheritance (№R-24).

## Maintenance

re-derive after gazetteer syncs (pleiades/trismegistos/cigs — the stale-ingest guard enforces freshness) or place-moving catalog events; the collection digest in the recipe makes an unchanged projection a fingerprint no-op

## Provenance

Canonical inputs at derivation:

- `cigs` @ `29878f18cc54b523aa86887a3ec25505b5523e21280f215280c39224ad063c54`
- `pleiades` @ `d5170d25c3a3e6ad8f950922d0099f2c05c74aa074a64ea8962aef72b361b310`
- `trismegistos` @ `c935b7e95adcc403edb8ad18da4082234b9d4b30ee80ffc76bcceba09b53b3cf`

Recipe: places-lpf v1: LPF v1.3 FeatureCollection + LP-TSV v0.5 at claim grain over the published axis slice (license classes open+attribution), titles/coords from place_index, closeMatch from place_crosswalk; collection sha256=6f6661539011221981a7dfae54272e8d95a662b655040287f05a1093e76a6ab4

Derivation fingerprint: `857cb9d51a1eab27bce281c21ea28259c67c2510116699b7ccd9d01fddb5cc3d`.
