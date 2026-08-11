# The Egyptian sign spine — Unikemet codepoints with Gardiner codes and tool concordances

`egy/unikemet-signs` — gold-derived tier, anchoring: none. Produced by `nabu data build egy/unikemet-signs` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

## Why this dataset exists — in plain terms

The complete Unicode inventory of Egyptian hieroglyphs as one reference table: for each of the encoded signs, its Gardiner-style catalog code, what it depicts, how it functions (logogram, phonogram, classifier), its sound values, and the concordance codes the standard Egyptological tools (JSesh, Hieroglyphica, IFAO) use — the join spine for any digital Egyptology pipeline, flattened verbatim from the Unicode Unikemet data file.

Flattens Unikemet.txt to one row per encoded Egyptian hieroglyph — the Gardiner-style kEH_Cat code, the original Hieroglyphica-era kEH_UniK code, core/legacy status, description, functions, sound values, and the JSesh/Hieroglyphica/IFAO concordances every Egyptological tool joins on (the same spine Nabu's hiero card and the Edubba overlay key against). Every cell verbatim; absent tags stay empty. Permissive input (Unicode License V3) → clean CC BY 4.0.

## Maintenance

re-derive after `nabu sync unikemet` (upstream moves at annual Unicode releases); mechanical, no review needed beyond spot-checks

## Provenance

Canonical inputs at derivation:

- `unikemet` @ `71ed7b909ee1d5aa198e5e423ff9c29e5e92ceabe21fdaa9fcbbebc6f7a7c185`

Recipe: unikemet-signs v1: flatten Unikemet.txt to one row per codepoint, tag values verbatim (multi-occurrence tags ;-joined), file order

Derivation fingerprint: `dae4d9e5083abf2c506c08bcfe1ef86b279c954d2a6e38b9fe713c6f3fb6774c`.
