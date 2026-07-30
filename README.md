# nabu-data

Derived linguistic datasets over ancient-language corpora — form→lemma
tables, segmentation layers, metrical scansions, script-neutralization
and orthography fold tables, curated loanword and glyph censuses —
grouped by language, each independently loadable with one `read_csv`
call.

Every dataset here is produced by [Nabu](https://github.com/arvicco/nabu),
a local-first research store for ancient-text corpora, and carries its
full derivation provenance: the exact upstream corpus version (git sha),
the exact producing code version, and the recipe — re-runnable end to
end. Datasets that annotate specific passages anchor them by stable
Nabu URN **and** per-passage content hash, so a consumer can verify the
annotation still matches the text it was made from. Where a dataset
rests on an automatic process, its measured error rate is published
in-band (the manifest's `nabu.eval` block), not hidden.

## Layout

```
<language-code>/          ISO 639-3-based (san, xct, grc, …)
  <feature>/
    datapackage.json      Frictionless Data Package v2 manifest
                          (schema, license, attribution chain,
                          Nabu provenance block, eval where relevant)
    README.md             what / why / how to load / how to cite
    *.csv                 the data (CLDF-compatible nomenclature)
    sources.bib           upstream attribution, BibTeX
```

Sentence-shaped datasets additionally ship CoNLL-U projections. Honesty
labels ride in-band: every dataset states its tier (gold / gold-derived
vs silver/automatic) in the manifest and, where relevant, per row.

## Datasets

| Dataset | Content | License | Status |
|---|---|---|---|
| `san/form-lemma` | Sanskrit form→lemma table derived from DCS gold annotations — 428,825 rows + 98,538-entry lemma sidecar, DCS LemmaIds carried verbatim | CC BY 4.0 | **published** |
| `xct/wylie-fold` | Tibetan script ↔ EWTS (Wylie) transliteration rule table — 95 rules, the source of Nabu's generated Tibetan transcoder | CC BY 4.0 | **published** |
| `xct/verb-lemma` | Tibetan verb stem→paradigm-lemma map from the Tibetan Verb Database — 3,889 rows, grammarians' disagreements kept uncollapsed | CC BY 4.0 | **published** |
| `xct/segmentation` | Segmented Classical Tibetan, curated slice (SOAS gold texts + the Heart Sutra) — 319,162 URN+sha-anchored rows; boundary F1 0.9621 vs SOAS gold published in-band | CC BY 4.0 | **published** |
| `grc/meter` | Greek metrical scansions (Hypotactic) anchored to Perseus CTS passages — ~33,000 rows + the filename→CTS works crosswalk | CC BY 4.0 | **published** |
| `zho/hani-fold` | Han traditional↔simplified↔z-variant fold table from Unihan — 6,050 pairs plus the 477-row refusal census | CC BY 4.0 | **published** |
| `jpn/aozora-gaiji` | Aozora Bunko gaiji composition-formula census — 582 formulas with the 244-entry derived IDS lane | CC BY 4.0 | **published** |
| `jpn/kyujitai-fold` | Kyūjitai↔shinjitai fold table (Unihan jinmeiyō + KANJIDIC2 lanes) — 741 pairs | CC BY-SA 4.0 | **published** |
| `lzh/kanripo-gaiji` | The Kanripo gaiji display ladder — 427 faithful mappings + 562 substitutes, hand-curated over KR-Gaiji | CC BY-SA 4.0 | **published** |
| `lat/sabellic-loans` | Sabellic (Oscan/Umbrian/Sabine) → Latin loanword table — 85 lemmas with relation flags and Old Italic etyma | CC BY-SA 4.0 | **published** |
| `sux/value-signs` | Cuneiform value→sign table flattened from the Oracc Sign List (ex-OGSL, CC0) — one row per (value, sign) pair with codepoints, deprecation and ambiguity in-band, plus sign and print-concordance sidecars | CC BY 4.0 | **published** |

## Licensing

The repository's default license is [CC BY 4.0](LICENSE), and most
datasets carry it. **Some datasets are CC BY-SA 4.0 instead** — they
derive from share-alike upstreams (Wiktionary, KANJIDIC2/EDRDG,
KR-Gaiji) and inherit that condition; each such dataset says so
explicitly in its `datapackage.json` and README, and for those the
repository default does not apply. **The per-dataset manifest is
always the authoritative license statement.** Nothing here derives
from non-commercial or no-derivatives sources — such inputs are
disqualifying by policy.

Each dataset's manifest and `sources.bib` name the upstream works it
derives from and their licenses — cite those alongside this
repository. Repository citation metadata: [CITATION.cff](CITATION.cff).
Versioned releases will carry Zenodo DOIs; cite the version DOI of the
release you used.

## The two-way loop

Nabu itself consumes this repository as a registered source: the
published form→lemma table feeds Nabu's Sanskrit dictionary lookup
through the same ingestion front door as any upstream corpus. The
reproducibility loop is closed in public.
