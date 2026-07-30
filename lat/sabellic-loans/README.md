# Sabellic → Latin loanword table (en.wiktionary curation)

`lat/sabellic-loans` — gold tier, anchoring: none. Produced by `nabu data build lat/sabellic-loans` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

Flattens the hand-curated Sabellic (Oscan/Umbrian/Sabine) → Latin loan rows — 85 Latin lemmas with borrowed/derived relation flags and the Old Italic etyma en.wiktionary cites — into one reusable table; the same curation powers Nabu's sabellic-osc/xum/sbv dictionary shelves and their loan-flagged etymology edges. CC BY-SA (the Wiktionary share-alike grant — owner ruling D51-a).

## Maintenance

on re-curation of config/sabellic_loans.yml only (a deliberate repo change, not a sync); each curation change re-fingerprints the dataset via the recipe's embedded file sha

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: sabellic-loans v1: config/sabellic_loans.yml (sha256 4d93ef54fa8fc35bf729df9af0fbacd2984d88d3cb0850f24315784a1adb5b95) flattened to one row per curated Latin lemma × Sabellic source language, YAML order kept; Relation verbatim from the curation (borrowed = explicit category membership, derived = superset-only), etyma and transliterations verbatim (leading * = reconstructed, empty = no form cited), values NFC-normalized; ID = <source language>-<Latin lemma>.

Derivation fingerprint: `975dcb1320633d0d8cdac2028168de648094ec7b37055ef21b4eb60f59ab9c6a`.

## The curation

Rows are curated by hand from the en.wiktionary category pages
"Latin terms borrowed from / derived from Oscan · Umbrian · Sabine"
(member lists via the MediaWiki API; retrieval date in every
citation), with each Latin entry's OWN {{bor|la|…}}/{{der|la|…}}
etymology template read for the source-language etymon. Census:
85 rows — Oscan 48 (23 borrowed), Umbrian 11 (6), Sabine 26 (13).
The same curation file powers Nabu's sabellic-osc/xum/sbv dictionary
shelves and their borrowed-flag etymology edges.

## Columns and semantics

`Form` is the Latin lemma; `Language_ID` is `lat` throughout — the
loans live in Latin, and `languages.csv` carries that one row.
`Etymon_Language` names the Sabellic source in ISO 639-3: `osc`
Oscan (osca1244), `xum` Umbrian (umbr1253), `sbv` Sabine
(sabi1245). `Relation` is the curation's closed vocabulary,
verbatim: `borrowed` = the lemma sits in the explicit "borrowed
from X" category; `derived` = only in the "derived from X" superset
(indirect or unspecified transmission — never a guess). `Etymon`
carries the cited source-language form verbatim (Old Italic script
where en.wiktionary gives it; a leading `*` marks a reconstructed
etymon); an empty cell means no source-language form is cited —
absence is honest, never filled in. `Etymon_Translit` is the
curated transliteration where one is recorded.

## Licensing

Upstream is dual-licensed CC BY-SA 4.0 + GFDL (the Wiktionary
grant); this dataset publishes under CC BY-SA 4.0, the one honest
single choice — see the License line above and each citation's note.

## Loading

    import pandas as pd
    df = pd.read_csv("loans.csv", keep_default_na=False)
