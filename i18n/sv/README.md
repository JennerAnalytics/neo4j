# Neo4j och nätverksanalys med Jenner

[Jenner](https://jenneranalytics.com) tar in grafdatabaser och
nätverksanalys i den SAS-kompatibla världen av DATA-steg och PROC.
Anslut till **Neo4j** eller **Memgraph** med ett `LIBNAME`, fråga dem
med **Cypher/GQL**, kör graf**algoritmer**, rita **interaktiva
nätverksdiagram** och använd ändå de **SAS-kompatibla** procedurerna
för nätverksoptimering och -analys — allt i ett och samma program.

Det här repot visar hela stacken, förankrad i en verklighetsnära
flaggskeppsnotebook och en visualiseringsdemo utan databas. Allt
tillhandahålls på **15 språk** (se [Språk](#språk)).

## Funktioner

### Nytt — Jenners graffamilj (ingen SAS-motsvarighet)

| Funktion | Vad den gör |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (eller `MEMGRAPH`) | Binder en grafdatabas till ett libref, som vilket annat bibliotek som helst. |
| **`PROC GQL`** | Kör **Cypher/GQL**-frågor mot grafen och skriver resultatmängden till ett Jenner-dataset. |
| **`PROC LINKS`** | Kör graf**algoritmer** — PageRank, gemenskapsdetektering, kortaste väg, centralitet — mot grafen och skriver resultat per nod/kant till ett dataset. |
| **`PROC NETVIZ`** | Renderar en graf som ett **interaktivt nätverksdiagram med Cytoscape.js** (inline i Jupyter-kärnan, eller som en fristående HTML-fil från CLI:t). |

### SAS-kompatibla nätverksprocedurer

| Funktion | Vad den gör |
|---|---|
| **`PROC OPTNET`** | Nätverks**optimering** över Jenner-dataset — kortaste väg, TSP, minkostnadsflöde, sammanhängande komponenter, cykler, klickar med mera. En portning av SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Klassisk nätverks**analys** över Jenner-dataset — centraliteter, gemenskaper, tvåfaldigt sammanhängande komponenter, vägar. En portning av SAS Viya PROC NETWORK. |

Den nya familjen arbetar mot en **levande grafdatabas**; de
SAS-kompatibla procedurerna arbetar mot **länk-/noddataset** som du
redan har. De går att kombinera: hämta en delgraf med `PROC GQL`,
poängsätt den med `PROC LINKS` eller `PROC NETWORK`, optimera med
`PROC OPTNET` och rita den med `PROC NETVIZ`.

## Flaggskeppsnotebook — bedrägerianalys av ICIJ offshore-leaks

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
kör en komplett pipeline för bedrägerianalys mot den **verkliga
läckan ICIJ Paradise Papers** (163 435 noder — offshore-entiteter,
befattningshavare, adresser och mellanhänder). Den ansluter med
`LIBNAME … GRAPH ENGINE=NEO4J`, utforskar med `PROC GQL` och
poängsätter risk med `PROC NETWORK` — ett komplett, databasstött
grafarbetsflöde.

> Notebooken ansluter till en Neo4j-graf (Jenner Workspace-plattformen
> är värd för ICIJ-datasetet). Rikta `LIBNAME` mot din egen
> Neo4j/Memgraph för att köra den mot dina egna data.

## Visualiseringsdemo — ingen databas krävs

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/)
renderar en graf över offshore-ägande som ett interaktivt
nätverksdiagram från vanliga dataset — kör den med enbart `jenner`-CLI:t:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Nätverksdiagram med PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Krav

- `jenner`-binären på din `PATH`.
- För graffamiljen (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): en
  nåbar **Neo4j**- eller **Memgraph**-instans, och en `jenner` byggd
  med funktionen `neo4j`.
- `PROC NETVIZ`-demon och de SAS-kompatibla procedurerna kräver ingen
  databas.

## Struktur

```
notebooks/en/   flaggskeppsnotebooken för ICIJ (engelska)
demos/          netviz_showcase — nätverksdiagramdemo utan databas
i18n/<språk>/   lokaliserad README + notebook per språk
```

## Språk

Varje språkmapp har en lokaliserad README och en översatt notebook:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Licens

MIT. ICIJ-data är © ICIJ och används enligt deras villkor; se notebooken.
