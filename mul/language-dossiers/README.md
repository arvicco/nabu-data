# Curated language dossiers — the human-written name/family/context per language

`mul/language-dossiers` — curated tier, anchoring: language-code. Produced by `nabu data build mul/language-dossiers` (Nabu 1.5.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-SA-4.0 (https://creativecommons.org/licenses/by-sa/4.0/). This dataset is CC BY-SA 4.0 (inherited share-alike from its inputs); the repository's default license does not apply to it.

## Why this dataset exists — in plain terms

What does Nabu actually know about each of its languages — the language's name, where it sits in its family, and a paragraph of human-written context? This dataset publishes those curated language dossiers, so a freshly installed Nabu shows the same context the original curator wrote rather than a bare code. Each row is one attribute (name, family, a context paragraph, or its provenance) of one language, cited by its Nabu language code. Much of the context prose is adapted from Wikipedia, which is why the whole dataset is share-alike (CC BY-SA 4.0); each dossier's provenance travels beside it.

Fixes the replicability gap the curated dossiers left behind: the hand-authored name/family/context lanes lived only in the originating instance's local/ shelf, so a fresh install saw bare language codes. Published as an overlay (re-consumed via `nabu sync nabu-data`), every install composes the same curated context beneath its live holdings and lect ladder. Only the non-derivable curated layer travels — section accretions (iecor varieties, corpus witnesses, the lect stage ladder) are excluded, each install rebuilds them from its own synced sources. CC BY-SA 4.0: ~71% of the context prose is Wikipedia-derived (share-alike), so the whole dataset inherits it (№R-48); the Wikipedia-derived share is censused in nabu.eval, and personal notes ride the private `nabu note` layer, never here.

## Maintenance

re-derive after curating dossiers (owner front-matter/context edits, the coming `nabu note` language layer); the published-slice digest makes an unchanged dossier corpus a fingerprint no-op

## Provenance

Own authorship — no canonical corpus inputs.

Recipe: language-dossiers v1: publish the curated dossier layer (name, family, context, extra lanes, provenance) from local/shelves/local-language, one CLDF ValueTable row per (code, attribute), code order; section accretions (iecor/witness/lect-ladder) excluded as per-install derivable; published-slice sha256=afc708bbdb1816a2fac6cbc74b1e3a9ca43958e1d671fc1213e7d828eb87895a

Derivation fingerprint: `dc20efe7e630059ad0965d344eacf8c57df83679f9fedcd7a918e0483b678ad7`.
