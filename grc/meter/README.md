# Greek metrical scansions (Hypotactic) anchored to Perseus CTS passages

`grc/meter` — gold-derived tier, anchoring: passage-urn. Produced by `nabu data build grc/meter` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

Publishes D. Chamberlain's Hypotactic scansions (CC BY 4.0) as rows citable at urn:cts:greekLit grain: upstream has no citation scheme (work = filename, line = file order), so the URN + Passage_SHA256 anchoring Nabu derives by exact folded-text match IS the added value — with the matched/unmatched census published in-band and the row text taken from Hypotactic's own bytes, never the CC BY-SA Perseus text.

## Maintenance

re-derive after hypotactic / perseus-greek / first1k-greek syncs (the stale-ingest guard enforces freshness); each release republishes the resolution census in nabu.eval

## Provenance

Canonical inputs at derivation:

- `first1k-greek` @ `8ee111eb44ecef4120c844e10749178d95d1f30c`
- `hypotactic` @ `d167c561107fc636ffd00198ffd1296edaf93451`
- `perseus-greek` @ `df7270e5df9c6e4e14c85a11a0a4b7f4a1a9f59e`

Recipe: grc/meter v1: resolve every line of canonical/hypotactic/tsv/*.tsv (D. Chamberlain's Greek scansions; the file NAME carries the work via the curated filename→CTS crosswalk published as works.csv — upstream has no citation column) onto the held live grc passages of perseus-greek + first1k-greek by EXACT folded-text match (the house grc search-form fold reduced to letters only; no fuzzy matching — unmatched lines are censused in nabu.eval, never guessed); one row per anchored passage (Homer's verbatim formulaic repeats dedupe to the first-held occurrence; a repeated line still counts as matched); Primary_Text carries Hypotactic's own TSV line bytes (CC BY 4.0), NEVER the Perseus/First1K passage bytes (those corpora are CC-BY-SA — anchoring is by URN + Passage_SHA256 only, so no share-alike text enters this CC BY dataset).

Derivation fingerprint: `91f35032d6c35740cc1da167b76da381ab992bf8552fb5e6ee4893f325de347b`.

## What a row means — the anchoring contract

Each row anchors one of Hypotactic's expert scansions to one held Greek
line: `URN` names the CTS passage, `Passage_SHA256` the exact bytes of
that passage in the corpus it was derived against. Rows apply only where
the passage sha matches — if a corpus edition moves, re-derive rather
than trust stale anchors. `Primary_Text` is the Greek line **from
Hypotactic's own CC BY 4.0 TSV** — deliberately never the Perseus/First1K
passage bytes, because those corpora are CC BY-SA and this dataset is
CC BY: the anchor is a fact (URN + sha), the text is Chamberlain's.
`Meter`/`Pattern`/`Caesura` are the TSV's own columns verbatim (the
caesura cell is empty when the line carries none).

## The crosswalk sidecar

Upstream files carry no citation scheme (work = filename, line = file
order). `works.csv` publishes the curated filename→CTS crosswalk this
dataset resolves through — own curation, factual id maps; `URN_Prefix`
is the exact resolution grain (a bare textgroup prefix spans every held
work under it).

## The resolution census — the honesty stat

34370 of 62989 upstream lines
(54.57%) resolved onto
33156 held passages
(79 works matched, 9 files
unmatched);
28619 lines found no held passage and are
censused, never guessed. Matching is exact on the folded letter sequence
(accents/breathings/punctuation/elision spelling neutralized) — the same
numbers ride `datapackage.json` under `nabu.eval`.

## Loading

    import pandas as pd
    df = pd.read_csv("meter.csv", keep_default_na=False)

How to cite: reference David Chamberlain and hypotactic.com (the
`hypotactic` key in `sources.bib`) alongside this dataset's
`datapackage.json` provenance block.
