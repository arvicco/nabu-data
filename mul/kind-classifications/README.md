# Per-document kind classifications (the fourth axis) across the multilingual catalog

`mul/kind-classifications` — gold-derived tier, anchoring: document-urn. Produced by `nabu data build mul/kind-classifications` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

What KIND of text is each ancient document — an epitaph, a receipt, a hymn, a school exercise? This dataset publishes Nabu's fourth document axis across its whole multilingual catalog: for each classified document (cited by its stable URN), the ruled cross-corpus class path (a 21-family list with named sub-classes, e.g. funerary/epitaph, literary/poetry, divination/extispicy), multi-label as multiple rows, together with the verbatim upstream genre label each fold was derived from — one uniform classification table instead of a dozen per-corpus genre jargons.

Publishes the classification layer behind Nabu's kind axis (№R-63/№R-66) — per-document ruled class paths (a 21-family cross-corpus list with named sub-classes: funerary/epitaph, literary/poetry, divination/extispicy, ...), multi-label as multiple rows, the VERBATIM upstream genre label riding every row so each fold is checkable against its source. The honest `unknown` class publishes; the `unmapped` curation bucket does not (a TODO marker is not a classification). License classes open+attribution only (nc slices excluded row-by-row, censused in nabu.eval); CC BY-SA 4.0 — the №R-24 carve-out carrying the share-alike lanes.

## Maintenance

re-derive after classification-moving events (new kind_map folds, a class tree change, a re-projection) — the published-slice digest makes an unchanged projection a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: kind-classifications v1: project facet=kind document_facets rows at URN grain (config/kind_classes.yml + kind_map.yml folds, №R-63/№R-66), license classes open+attribution only, unmapped excluded, ordered (urn, facet row); published-slice sha256=220b7184ccca5d5ffd962c7710c29ee3c12bb6f899424e80248c696d113d5187

Derivation fingerprint: `1aa7332d1e71df60b5164133f9d100a109bbd9ad2eb2136c397eb393a5d85799`.
