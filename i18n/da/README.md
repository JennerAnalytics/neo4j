# Neo4j & netværksanalyse med Jenner

[Jenner](https://jenneranalytics.com) bringer grafdatabaser og netværks-
analyse ind i den SAS-kompatible DATA-trins- og PROC-verden. Opret forbindelse til **Neo4j**
eller **Memgraph** med et `LIBNAME`, forespørg dem med **Cypher/GQL**, kør graf-
**algoritmer**, tegn **interaktive netværksdiagrammer**, og brug stadig de
**SAS-kompatible** procedurer til netværksoptimering og -analyse — alt sammen i ét
program.

Dette repository viser hele stakken, forankret af en flagskibs-notebook fra den
virkelige verden og en visualiseringsdemo uden database. Alt leveres på
**15 sprog** (se [Sprog](#sprog)).

## Funktioner

### Ny — Jenners graf-familie (ingen SAS-ækvivalent)

| Funktion | Hvad den gør |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (eller `MEMGRAPH`) | Bind en grafdatabase til et libref, ligesom ethvert andet bibliotek. |
| **`PROC GQL`** | Kør **Cypher/GQL**-forespørgsler mod grafen og skriv resultatsættet til et Jenner-datasæt. |
| **`PROC LINKS`** | Kør graf-**algoritmer** — PageRank, fællesskabsdetektion, korteste sti, centralitet — mod grafen og skriv resultater pr. knude/pr. kant til et datasæt. |
| **`PROC NETVIZ`** | Gengiv en graf som et **interaktivt Cytoscape.js**-netværksdiagram (inline i Jupyter-kernen eller en selvstændig HTML-fil fra kommandolinjen). |

### SAS-kompatible netværksprocedurer

| Funktion | Hvad den gør |
|---|---|
| **`PROC OPTNET`** | Netværks**optimering** over Jenner-datasæt — korteste sti, TSP, minimum-cost flow, forbundne komponenter, cykler, kliker og mere. En port af SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Klassisk netværks**analyse** over Jenner-datasæt — centraliteter, fællesskaber, biforbundne komponenter, stier. En port af SAS Viya PROC NETWORK. |

Den nye familie arbejder på en **live grafdatabase**; de SAS-kompatible
procedurer arbejder på **kant-/knude-datasæt**, du allerede har. De spiller sammen:
hent en delgraf med `PROC GQL`, score den med `PROC LINKS` eller `PROC NETWORK`,
optimér med `PROC OPTNET`, og tegn den med `PROC NETVIZ`.

## Flagskibs-notebook — ICIJ offshore-leaks bedrageri-analyse

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
kører en komplet pipeline til bedrageri-analyse mod det **reelle ICIJ Paradise
Papers**-læk (163.435 knuder — offshore-selskaber, officerer, adresser og
mellemmænd). Den opretter forbindelse med `LIBNAME … GRAPH ENGINE=NEO4J`, udforsker med
`PROC GQL` og scorer risiko med `PROC NETWORK` — et komplet, databasebaseret
graf-workflow.

> Notebooken opretter forbindelse til en Neo4j-graf (Jenner Workspace-platformen hoster
> ICIJ-datasættet). Peg `LIBNAME` mod din egen Neo4j/Memgraph for at køre den
> mod dine egne data.

## Visualiseringsdemo — ingen database påkrævet

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) gengiver en graf over
offshore-ejerskab som et interaktivt netværksdiagram ud fra almindelige datasæt — kør den med blot
`jenner`-kommandolinjen:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ-netværksdiagram](../../demos/netviz_showcase/images/example_netviz.png)

## Krav

- `jenner`-binæren på din `PATH`.
- Til graf-familien (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): en tilgængelig
  **Neo4j**- eller **Memgraph**-instans og en `jenner` bygget med `neo4j`-
  funktionen.
- `PROC NETVIZ`-demoen og de SAS-kompatible procedurer kræver ingen database.

## Struktur

```
notebooks/en/   flagskibs-ICIJ-notebooken (engelsk)
demos/          netviz_showcase — netværksdiagram-demo uden database
i18n/<sprog>/   lokaliseret README + notebook pr. sprog
```

## Sprog

Denne fil er den danske oversættelse. Se [alle 15 sprog](../../README.md) i
hoved-README'en, hvor hver sprogmappe har en lokaliseret README og en
oversat notebook.

## Licens

MIT. ICIJ-dataene er © ICIJ og bruges under deres vilkår; se notebooken.
