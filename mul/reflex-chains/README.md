# Reconstruction→reflex edges of the held etymological dictionaries, joined to the gold corpus

`mul/reflex-chains` — gold-derived tier, anchoring: none. Produced by `nabu data build mul/reflex-chains` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

Etymological dictionaries tell you that Proto-Germanic *hlaibaz became Gothic hlaifs, Old English hlāf and Old Norse hleifr — but not whether those descendant words actually occur in the surviving texts. This dataset publishes every reconstruction→reflex edge of the openly licensed etymological dictionaries Nabu holds (Wiktionary's reconstruction pages, the Tower of Babel databases, IE-CoR, WOLD and smaller lanes) as one table, and joins each reflex to Nabu's human-verified (gold) lemmatized corpus: when the reflex is a lemma of the held corpus in that language, the row says how many passages attest it. That linkage from reconstructed roots to attested text is what no etymological database publishes.

Every reconstruction→reflex edge of the held etymological dictionaries (Wiktionary reconstruction shelves, the Tower of Babel databases, IE-CoR, WOLD and smaller lanes) as one table — dictionary, entry headword, the reflex's upstream language code verbatim and its catalog code, the reflex verbatim with romanization and both folded forms, borrowed/uncertain edge flags carried through — plus the join no etymological database publishes: Attested, the gold passage attestations whose folded lemma EQUALS the reflex's folded form (else its folded romanization, the script bridge) under the same catalog language code — the rule Nabu's etym desk resolves at query time, stored-key equality only, no fuzzy or cross-language matching; match/miss censused per language in nabu.eval. License screening row-by-row: open+attribution dictionary sources only — nc dictionaries (derom, mw, edl) are excluded and censused per class and source, and only gold rows of publishable sources count toward Attested; CC BY-SA 4.0 — Wiktionary's share-alike grant dominates (the share-alike carve-out).

## Maintenance

re-derive after dictionary-shelf syncs (wiktionary-recon, starling, iecor, wold, ...) or lemma-moving events (treebank syncs, a rebuild or builders:refresh re-projecting the rollup); the published-slice digest makes an unchanged slice a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: reflex-chains v1: project dictionary_reflexes of live entries at (dictionary, entry, seq) grain, license classes open+attribution only, ordered (dictionary, entry id, seq); Attested = sum of lemma_rollup grade gold occurrences from open+attribution sources whose folded lemma equals the reflex word_folded, else roman_folded, under the same catalog language code (stored-key equality only); published-slice sha256=898086b03d8cafffbbd3956f1ecfebcb130a6a3c9b6236d30577136795ec8039

Derivation fingerprint: `e1fba7a0337e82e32db90e7a0540066b10d22d54eac76f0dfb4114c4d5d67898`.

## The Attested join rule

`Attested` is mechanical and deliberately narrow: the sum of GOLD
passage attestations (one per distinct lemma per passage) whose
folded lemma key is EQUAL to the reflex's `Form_Folded` — or, when
that finds nothing, its `Roman_Folded` (the script bridge: a
Gothic-script reflex joins the romanized gold lemma) — under the SAME
catalog language code (`Language_ID`). `Attested_Via` names the key
that matched (`form` | `roman`). No fuzzy matching, no cross-language
matching, no re-folding; only gold lemmatization from openly licensed
corpora counts (automatic lemmatization and non-commercial corpora
never enter the integer). An empty cell means "not attested in the
held gold corpus under this rule" — never a zero claim. Rows with an
empty `Language_ID` are display-only nodes (an upstream code with no
catalog counterpart) and are never joined. nabu.eval carries the
attested/missed census per language.

## Columns

`Headword` is the dictionary entry's headword verbatim with its
object language in `Headword_Language` — the reconstruction on the
proto shelves, the attested word on the attested-language and
loanword shelves. `Lang_Code` is the upstream language code verbatim;
`Seq` the depth-first position of the node in the entry's descendant
tree. `Borrowed` / `Uncertain` are the upstream edge markers: `true`,
`false`, or empty (the row predates the flag-aware parse — unknown,
never a claimed false).
