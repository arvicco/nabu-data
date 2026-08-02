# Cantigas Medievais Galego-Portuguesas — the Littera edition as structured tables (verse lines, cantigas, authors, cancioneiro concordance)

`roa-opt/cantigas` — gold tier, anchoring: urn+sha. Produced by `nabu data build roa-opt/cantigas` (Nabu 1.4.0); the producer-side contract is docs/nabu-data.md in the Nabu repository.

License: CC-BY-4.0 (https://creativecommons.org/licenses/by/4.0/).

## Why this dataset exists — in plain terms

The cantigas are the songs of the medieval Galician-Portuguese lyric
— the courtly cantigas de amor, the female-voiced cantigas de amigo,
and the satirical cantigas de escárnio e maldizer, plus rarer forms
(lais, tenções, pastorelas), composed at the Iberian courts across
the 13th and 14th centuries. About 1,680 of them survive, by some
160 named troubadours and jograis — kings among them — transmitted
in three great songbooks, the cancioneiros (Ajuda, Biblioteca
Nacional, Vaticana). This is the complete secular corpus of one of
medieval Europe's major lyric traditions.

The reference edition of that corpus is Cantigas Medievais Galego
Portuguesas (cantigas.fcsh.unl.pt), the Littera project's critical
edition by Graça Videira Lopes, Manuel Pedro Ferreira and their team
at the Instituto de Estudos Medievais (FCSH/NOVA, Lisbon). It is a
superb scholarly database — and it is browser-only: no TEI, no
export, no API; every cantiga lives on a web page. Anyone wanting to
compute over the corpus — trace an author, count refrains, join the
songs to their manuscripts — had no machine-readable edition to
stand on.

This dataset is that edition: every verse line, every cantiga, every
author and every manuscript witness, as plain tables. It exists
because the project's coordinator granted it in writing ("Our site
is free for all. So, with full attribution, you can do whatever you
like with the data") — so the project's own citation format rides
every file here, and using this data means citing the edition.

The manuscripts table adds the piece the database never shows in one
place: the corpus-wide concordance of which cantiga survives in
which cancioneiro under which number — the join surface for
manuscript-transmission questions across the whole tradition.

The first full-corpus re-publication: the complete secular lyric of medieval Galician-Portuguese — ~1,680 cantigas, ~34K verse lines from the three great cancioneiros — projected from the Littera critical edition (cantigas.fcsh.unl.pt) into the corpus's first machine-readable form (the scholarly database is superb and browser-only: no TEI, no export), under the coordinator's written any-use grant (№45-2) with the project's own citation format riding every file — verse lines anchored urn+sha into the catalog, the cantiga/author registries, and the corpus-wide cancioneiro concordance parsed from the edition's manuscript sigla, with the citation-fidelity census (printed-number confirmations, refrain gaps, empty lines, the unattributed page) published in-band as nabu.eval.

## Maintenance

re-derive after a cantigas re-sync (Littera is a living edition that corrects pages in place; the stale-ingest guard enforces freshness); every build re-derives the citation-fidelity census into nabu.eval

## Provenance

Canonical inputs at derivation:

- `cantigas` @ `46dcaac9688533c07ed3510bab87e5d0cdff113e787b390fcc86b0b15237ba33`

Recipe: roa-opt/cantigas v1: every live cantigas catalog row projected to four tables, documents in numeric cdcant order, passages in sequence order — lines.csv one row per verse line (URN + Passage_SHA256 anchor; Line/Stanza = the EDITION's own numbering, cross-checked against the printed every-5th ordinals at ingest; Number_Gap = the P56-1 refrain-gap annotation where the edition's numbering runs ahead of the display; Primary_Text = the passage bytes); cantigas.csv one row per cantiga (Cdcant, incipit, Author_ID -> authors.csv, normalized genre, '; '-joined form lines, rubric; the unattributed page keeps an empty Author_ID); authors.csv the distinct (cdaut, name) registry in cdaut order; manuscripts.csv one row per (cantiga, witness) from the sigla lines — commas split witnesses, '(…)' becomes Parenthesized=true, the leading capital run is Cancioneiro, the remainder is Number VERBATIM (a slash run like 575/576 stays ONE witness; bis/letter/= forms kept as printed; a bare siglum has an empty Number; anything else fails loudly). IDs l-<cdcant>-<line> / c-<cdcant> / a-<cdaut> / m-<cdcant>-<siglum>-<number>, positional -<n> on verbatim repeats.

Derivation fingerprint: `8fb9ee89a18cb1d7769c47cbe114d8098807a85771d29ff8e08571f542ee335a`.

## The tables — one edition, four projections

`lines.csv` is the corpus at verse grain, in cdcant order: `URN` +
`Passage_SHA256` name the exact catalog passage bytes (rows apply
only where the sha matches — the urn+sha anchoring contract);
`Line`/`Stanza` are the EDITION's own numbering (see the census
below); `Number_Gap` is non-empty exactly where the edition's
numbering runs ahead of the displayed text (refrain lines the page
display merges — the value is how many edition lines the display
skipped, riding the stanza's first line); `Primary_Text` is the
verse. `cantigas.csv` is one row per cantiga: `Cdcant` is Littera's
own stable id (the `cdcant=` URL parameter), `Incipit` the first
verse, `Author_ID` joins `authors.csv` (empty on the one
unattributed page), `Genre` the normalized genre facet, `Form` the
sidebar's formal description (`; `-joined), `Rubric` the
manuscript rubric where one exists. `authors.csv` is the distinct
troubadour/jogral registry with Littera's `Cdaut` ids. Join
`lines.Cantiga_ID` and `manuscripts.Cantiga_ID` on `cantigas.ID`.

## manuscripts.csv — the cancioneiro concordance

One row per (cantiga, manuscript witness), parsed from the
edition's *Fontes manuscritas* sigla lines. Comma-separated
witnesses become rows; the leading capital run is the
`Cancioneiro` siglum (A = Cancioneiro da Ajuda, B = Biblioteca
Nacional, V = Vaticana, C = the Tavola Colocciana index, plus the
edition's smaller sigla — N, T, L, P, E, TO, M at this census);
everything after it rides `Number` VERBATIM: a slash run
(`575/576`) is ONE witness spanning those numbers, never split;
`8bis`, `517b`, `29=38` and `1146 bis` keep their printed bytes; a
bare siglum (`P`) has an empty `Number`. A witness the edition
prints in parentheses (`(C 1)` — an index attestation, not a text
witness) keeps `Parenthesized` = `true`. One sidebar line is not a
witness at all: the literal "Não disponível" marker (the edition's
explicit statement that no manuscript source is available — one
cantiga at this census) yields no rows, and a cantiga whose page
carries no *Fontes manuscritas* section likewise has none. Any
other token outside this grammar fails the build loudly — the
concordance never guesses.

## The citation — the grant's one condition

This corpus is published with the written permission of the
project's coordinator (Graça Videira Lopes, 2026-07-27, license
thread №45-2): "Our site is free for all. So, with full
attribution, you can do whatever you like with the data." Use of
this dataset therefore carries the project's own citation format,
verbatim (fill the retrieval-date slot with the date you took this
dataset):

> Lopes, Graça Videira; Ferreira, Manuel Pedro et al. (2011–), Cantigas Medievais Galego Portuguesas [online database]. Lisboa: Instituto de Estudos Medievais, FCSH/NOVA. [Information retrieved on (date)] Available at: cantigas.fcsh.unl.pt.

## The census — citation fidelity (`nabu.eval`)

Of 34162 verse lines across 1682 cantigas:
6125 sit on the edition's printed every-5th
ordinals — each one verified against the printed number at ingest
(a mismatch quarantines the page, so the `Line` column IS the
edition's numbering); 7 lines open a refrain
number gap (8 edition lines counted but not displayed
upstream — the `Number_Gap` column); 1 edition line numbers
are consumed by numbered-but-textless rows upstream (censused in
the eval, no row minted); 1 cantiga(s) carry no author
attribution. The same numbers ride `datapackage.json` under
`nabu.eval`.

## The honest gap — cdcant 1066

One cantiga of the corpus, cdcant 1066, has no text in the edition
("Texto ainda não disponível" — a doubled apógrafo transcription
Littera has not yet published). It is quarantined at ingest and
appears in NO table here; when the edition publishes the text, a
re-sync and re-build will pick it up.

## Loading

    import pandas as pd
    lines = pd.read_csv("lines.csv", keep_default_na=False)
    cantigas = pd.read_csv("cantigas.csv", keep_default_na=False)
    corpus = lines.merge(cantigas, left_on="Cantiga_ID", right_on="ID",
                         suffixes=("", "_cantiga"))

How to cite: the Littera citation above (the `littera` key in
`sources.bib`) alongside this dataset's `datapackage.json`
provenance block.
