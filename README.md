# nabu-data

Derived linguistic datasets over ancient-language corpora — form→lemma
tables, segmentation layers, script-neutralization rules and related
content — grouped by language, each independently loadable with one
`read_csv` call.

Every dataset here is produced by [Nabu](https://github.com/arvicco/nabu),
a local-first research store for ancient-text corpora, and carries its
full derivation provenance: the exact upstream corpus version (git sha),
the exact producing code version, and the recipe — re-runnable end to
end. Datasets that annotate specific passages anchor them by stable
Nabu URN **and** per-passage content hash, so a consumer can verify the
annotation still matches the text it was made from.

## Layout

```
<language-code>/          ISO 639-3-based (san, xct, …)
  <feature>/
    datapackage.json      Frictionless Data Package v2 manifest
                          (schema, license, attribution chain,
                          Nabu provenance block)
    README.md             what / why / how to load / how to cite
    *.csv                 the data (CLDF-compatible nomenclature)
    sources.bib           upstream attribution, BibTeX
```

Sentence-shaped datasets additionally ship CoNLL-U projections. Honesty
labels ride in-band: every dataset states its tier (gold-derived vs
silver/automatic) in the manifest and, where relevant, per row.

## Status

Bootstrapping — first datasets land shortly:

| Dataset | Content | Status |
|---|---|---|
| `san/form-lemma` | Sanskrit form→lemma table derived from DCS gold annotations (~480K rows) | in preparation |
| `xct/wylie-fold` | Tibetan script ↔ EWTS neutralization rule table | in preparation |
| `xct/verb-lemma` | Tibetan verb stem→paradigm-lemma map (from the Tibetan Verb Database) | in preparation |
| `xct/segmentation` | Segmented Classical Tibetan, curated slice with published eval vs SOAS gold | planned |

## License and citation

All datasets: [CC BY 4.0](LICENSE). Each dataset's manifest and
`sources.bib` name the upstream works it derives from and their
licenses — cite those alongside this repository. Repository citation
metadata: [CITATION.cff](CITATION.cff). Versioned releases will carry
Zenodo DOIs; cite the version DOI of the release you used.

## The two-way loop

Nabu itself consumes this repository as a registered source — the
datasets published here feed back into its query surfaces through the
same ingestion front door as any upstream corpus. The reproducibility
loop is closed in public.
