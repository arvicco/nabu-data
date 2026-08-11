# nabu-data

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.21757475-blue.svg)](https://doi.org/10.5281/zenodo.21757475)


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
<language-code>/          ISO 639-3-based (san, xct, grc, …);
                          datasets spanning the whole multilingual
                          catalog file under mul/ (ISO 639-3's
                          special code "Multiple languages")
  <feature>/
    datapackage.json      Frictionless Data Package v2 manifest
                          (schema, license, attribution chain,
                          Nabu provenance block, eval where relevant)
    README.md             what / why / how to load / how to cite
    *.csv                 the data (CLDF-compatible nomenclature)
    sources.bib           upstream attribution, BibTeX
    LICENSE               only where the dataset's license differs
                          from the repository default (CC BY-SA
                          datasets carry their own license text)
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
| `xct/actib-anchors` | The first re-publication: stable anchors for ACTib's segmented eKangyur — 461,301 rows tying every Derge Kangyur passage (URN + content fingerprint) to its ACTib (volume, page, line), match census in-band (99.51% exact), plus the 2,245-row divergence/proofreading table | CC BY 4.0 | **published** |
| `roa-opt/cantigas` | The first machine-readable edition of the complete secular Galician-Portuguese lyric (Projeto Littera, by written grant) — 34,162 verse lines with stanza structure and citation-fidelity eval in-band, 1,682 cantigas, 158 authors, and the 3,333-row corpus-wide cancioneiro concordance | CC BY 4.0 | **published** |
| `mul/lect-assignments` | Per-document historical-stage (lect) assignments across the whole multilingual catalog — 482,287 URN-anchored rows with basis and note in-band; the corpus-scale stage stratification no other project publishes | CC BY-SA 4.0 | **published** |
| `mul/place-refs` | Per-document place references, gazetteer-ready — 969,929 (URN, namespaced claim) rows over 7,309 places, verbatim names and upstream-vs-registry basis in-band | CC BY-SA 4.0 | **published** |
| `mul/places-lpf` | The referenced places as Linked Places Format v1.3 + LP-TSV (the WHG upload shapes) — 7,309 Features with cited attested spellings, coordinates, when-spans and closeMatch links | CC BY-SA 4.0 | **published** |
| `mul/document-dates` | Normalized document datings — 703,372 signed year-span rows with the verbatim upstream dating string riding every row | CC BY-SA 4.0 | **published** |
| `mul/char-postings` | Han character × corpus doc-frequency census — 38,397 rows spanning Classical Chinese, Japanese, Old Tibetan and Old Japanese collections | CC BY-SA 4.0 | **published** |
| `sux/sign-table` | Compiled cuneiform sign cards — one row per OSL sign with codepoints, print-list numbers, CDLI readings and per-source attestation doc-counts over the open corpora | CC BY 4.0 | **published** |
| `egy/unikemet-signs` | The Egyptian sign spine — 5,067 Unicode hieroglyph codepoints with Gardiner-style codes, descriptions, functions, values and the JSesh/Hieroglyphica/IFAO concordances | CC BY 4.0 | **published** |

## Licensing

The repository's default license is [CC BY 4.0](LICENSE), and most
datasets carry it. **Some datasets are CC BY-SA 4.0 instead** — they
derive from share-alike upstreams (Wiktionary, KANJIDIC2/EDRDG,
KR-Gaiji) and inherit that condition; each such dataset says so
explicitly in its `datapackage.json` and README **and carries its own
`LICENSE` file** (the CC BY-SA 4.0 text) in its directory, and for
those the repository default does not apply. **The per-dataset
manifest is always the authoritative license statement.** Nothing here derives
from non-commercial or no-derivatives sources — such inputs are
disqualifying by policy.

Each dataset's manifest and `sources.bib` name the upstream works it
derives from and their licenses — cite those alongside this
repository. Repository citation metadata: [CITATION.cff](CITATION.cff).
Versioned releases carry Zenodo DOIs — the concept DOI
[10.5281/zenodo.21757475](https://doi.org/10.5281/zenodo.21757475)
always resolves to the latest version; cite the version DOI of the
release you used (v1.0.0, the first tagged release, cut in sync with
Nabu v1.4.0: [10.5281/zenodo.21757476](https://doi.org/10.5281/zenodo.21757476)).

## The two-way loop

Nabu itself consumes this repository as a registered source: the
published form→lemma table feeds Nabu's Sanskrit dictionary lookup
through the same ingestion front door as any upstream corpus. The
reproducibility loop is closed in public.
