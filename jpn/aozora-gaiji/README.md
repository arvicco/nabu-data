# Aozora Bunko gaiji composition census with derived IDS lane

`jpn/aozora-gaiji` — gold tier, anchoring: none. Produced by `nabu data build jpn/aozora-gaiji` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

The census of composition formulas Aozora Bunko transcribers wrote for glyphs Unicode cannot encode (582 distinct formulas, 1,129 occurrences at the 2026-07-22 snapshot), each with its occurrence count and resolution status, plus the 244-entry IDS lane a conservative structural grammar can prove — refusals classified per formula, never guessed: the gaiji display-honesty ladder, published.

## Maintenance

re-census on the owner's schedule as the corpus grows (the checked-in TSV header carries the snapshot provenance); each re-census re-fingerprints the dataset through the recipe's embedded sha256

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: aozora-gaiji v1: the checked-in composition-description census (config/gaiji/aozora-descriptions.tsv, sha256 bb5f4e6d1bca6b8b09eb9d13ed3a07c959bb352e506a5b7e31ecded9c71cee8e; snapshotted read-only from the live Aozora corpus — snapshot provenance in the TSV header) published as descriptions.csv (occurrence Count + Resolution status per formula, desc-sorted); ids.csv derives the IDS lane through Nabu::Ops::AozoraIdsBuilder — the SAME grammar `rake gaiji:aozora_ids` compiles for the display ladder (single ＋ between two literal Han ideographs → ⿰, single ／ → ⿱, everything else refused by class, never guessed); ID = g-<sha256(desc)[0,12]>

Derivation fingerprint: `1e075f0ef0ed99d61fc7c7601fbc224e7df2c286b8defad6285944befd9ea8e3`.

## What the census is

Aozora Bunko transcribers describe unencodable glyphs (gaiji) in-text
with composition formulas — ※［＃「口＋斗」…］ "mouth beside dipper".
descriptions.csv is the census of every DISTINCT composition formula
in the public-domain corpus (the parser's class-(c) unresolved-gaiji
annotations), with its live occurrence Count at the snapshot date and
its Resolution status. The checked-in census TSV is the dataset's
source of truth; its header carries the snapshot provenance (corpus
size, date), and this dataset re-fingerprints whenever the owner
re-censuses (the recipe embeds the TSV's sha256).

## The honesty bar for ids.csv

A derived ⿰AB is a STRUCTURAL claim (A-left, B-right), never an
identity claim and never a real codepoint. The grammar therefore
derives ONLY the mechanically unambiguous shapes — a single ＋ between
two literal Han ideographs (⿰), a single ／ (⿱) — and refuses
everything else, per class: `kana-component` (a radical NAME like
にんべん is not a component glyph), `replace` (「…」に代えて prose),
`subtractive` (旗－其＋冉 is arithmetic on parts, not IDS),
`parenthesised` (nested grouping), `multi-operator` (ambiguous
nesting), `other` (non-Han operands, malformed). Nothing is guessed;
the refusal classes are the map of what a future, braver derivation
would have to defend.

## Loading

    import pandas as pd
    census = pd.read_csv("descriptions.csv", keep_default_na=False)
    ids = pd.read_csv("ids.csv", keep_default_na=False)

`ID` is the primary key in both tables (`g-<sha256(Description)[0,12]>`
— the formula itself cannot survive the CLDF identifier class, so it
is digested); `Description` is also unique per table, and ids.csv rows
are exactly the `Resolution == "ids"` census rows.
