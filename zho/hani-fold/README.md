# Han traditional↔simplified↔z-variant fold table (from Unihan)

`zho/hani-fold` — gold-derived tier, anchoring: none. Produced by `nabu data build zho/hani-fold` (Nabu 1.3.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

The 6,050-pair Han fold resolved conservatively from Unihan's declared kTraditionalVariant/kSimplifiedVariant/kZVariant relations — the table that lets simplified-script queries reach the traditional-script canon (kanripo/cbeta), the same resolution `rake fold:hani` compiles into Nabu::Hani; every ambiguous fold is refused and published per-row with its reason, because the refusal census IS the curation.

## Maintenance

re-derive after each unihan sync (upstream /latest/ moves at annual Unicode releases); a changed table also re-derives Nabu's own Han fold via `rake fold:hani` — the conventions §9 rebuild caveat applies

## Provenance

Canonical inputs at derivation:

- `unihan` @ `8bf47834ffe25d222e298d4f8c890621546bd0b59e8be631c3dd28f2cb35eabf`

Recipe: hani-fold v1: canonical/unihan/Unihan_Variants.txt resolved through Nabu::Ops::HaniFoldBuilder — the SAME seam `rake fold:hani` compiles into Nabu::Hani (one resolution path, two consumers). kTraditionalVariant/kSimplifiedVariant/kZVariant only; kSemanticVariant, kSpecializedSemanticVariant and kSpoofingVariant are structurally excluded (different words / security data, never orthography). Conservative resolution: z-cluster union-find, single-target direct folds, multi-targets resolved only within one z-cluster, reverse-only kSimplifiedVariant evidence, chains composed to fixed points, cycles to the lowest codepoint; every ambiguity is REFUSED and published per-row in refusals.csv. Codepoints NFC at build; pairs sorted by variant codepoint; ID minted from the variant codepoint (U+4E9A → U-4E9A).

Derivation fingerprint: `0985e171ddd25e83facf63644ad80c6c40092985c8a4aa78358f93730a8091dc`.

## The census at this derivation

Unihan 17.0.0 (file date 2025-07-24):
6050 fold pairs — 5973 direct,
8 via z-cluster targets,
0 reverse-only, 70 z-cluster
members; 1 cycle(s) resolved to lowest codepoint.
Refused (published in refusals.csv): 477 —
414 self-listing,
63 multi-traditional,
0 multi-reverse,
0 trad-simp-conflict,
0 z-cluster-unmergeable.
Excluded structurally: 4063 semantic-variant
lines (never read into the graph).

## What the fold is (and is not)

Each pair maps a variant codepoint to its CANONICAL TRADITIONAL form —
the form the traditional-script corpora (kanripo, cbeta) store — so
simplified-script queries and traditional-script text meet on one
skeleton. It is an ORTHOGRAPHY table: only Unihan's
kTraditionalVariant / kSimplifiedVariant / kZVariant fields enter the
graph. The semantic-variant fields (kSemanticVariant,
kSpecializedSemanticVariant) name different words that mean the same
thing — folding them would be a lie — and kSpoofingVariant is security
data; all three are excluded structurally, never row-by-row.

Per-pair provenance kind (direct / z-cluster / reverse-only) is
deliberately not a column: chains compose to fixed points, so one
published pair can mix evidence kinds. The aggregate census above is
the honest grain.

## The refusals are the curation

Every ambiguous fold is refused and PUBLISHED in refusals.csv with its
reason: `self-listing` (the char lists itself among its traditional
variants — a traditional word in its own right; 了→瞭 would merge two
real words), `multi-traditional` (targets across distinct clusters —
发→發/髮 is a genuine merger; picking one is a guess),
`multi-reverse`, `trad-simp-conflict` (the two directional fields
disagree), and `z-cluster-unmergeable` (whose Form lists the whole
cluster's members). Consumers wanting a looser fold can relax exactly
the classes they accept.

## Language scope (the zho call)

languages.csv lists zho — the ISO 639-3 macrolanguage, the same
pan-CJK macro tag Nabu's own unihan shelf files under. Glottolog
assigns macrolanguages no glottocode, so that cell is honestly empty.
Inside Nabu the fold normalizes search for the Literary Chinese
corpora (lzh, och — kanripo/cbeta); it applies wherever Han
orthography variation crosses a query, and the one-language-per-
feature rail contract states that here instead of duplicating rows.

## Loading

    import pandas as pd
    pairs = pd.read_csv("pairs.csv")
    refusals = pd.read_csv("refusals.csv")

`ID` is the primary key in both tables; `Variant` is also unique in
pairs.csv (one fold per codepoint), and every `Traditional` value is a
fixed point — never itself a variant key.
