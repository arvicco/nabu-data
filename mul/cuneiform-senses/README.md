# Cuneiform sense glosses from Wiktionary (Sumerian, Akkadian, Hittite)

`mul/cuneiform-senses` — gold tier, anchoring: entry-urn. Produced by `nabu data build mul/cuneiform-senses` (Nabu 1.6.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

What do the words of the cuneiform world mean? This dataset republishes the sense glosses of Wiktionary's Sumerian, Akkadian and Hittite lanes (via the kaikki.org machine-readable extraction) as one uniform table: headword (cuneiform or romanized), language, part of speech, and the verbatim gloss, each row anchored by the library entry URN it was published from. The share-alike sidecar beside the CC-BY sux/sign-table core: sign lists and attestation counts there, senses here.

The BY-SA sense-lane sidecar the P73 sign-table deliberately deferred so its core could stay CC-BY: Wiktionary's sense glosses for the cuneiform languages (via the kaikki.org extraction), one row per sense — headword, language, POS, verbatim gloss, entry URN. Sign lists and attestation counts live in sux/sign-table (CC-BY); the share-alike senses live here, so neither license contaminates the other.

## Maintenance

re-derive after a kaikki shelf re-sync (owner-fired upstream refreshes; the stale-ingest guard enforces freshness)

## Provenance

Canonical inputs at derivation:

- `wiktionary-akk` @ `f0ce3d225a98d94c9cb8d05f189b27338af1cd11c887d16f912a5614985cd38b`
- `wiktionary-hit` @ `5c668aee83dc09dda06ad2de24174a66b92ce0db97c2ff541ff11afe2192bc41`
- `wiktionary-sux` @ `fc7df301cb53e1b52571dfc028775582f1cb70b5447616617ac8760758ef9657`

Recipe: cuneiform-senses v1: republish the sense glosses of the wiktionary-sux, wiktionary-akk, wiktionary-hit shelves verbatim, one row per sense, ordered (shelf, headword, entry); published-slice sha256=cea053837b4b49e85a6eb5a80cc1d1cf783167db91165d873f9058a0b5afc7bd

Derivation fingerprint: `26c089bde7a20f7fe1da47158b967e61306ad645a5b05b8c3eadf83cdcde2e04`.
