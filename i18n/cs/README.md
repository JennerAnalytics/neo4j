# Neo4j a síťová analýza s Jennerem

[Jenner](https://jenneranalytics.com) přináší grafové databáze a síťovou
analýzu do světa DATA kroku a procedur kompatibilního se SAS. Připojte se
k **Neo4j** nebo **Memgraph** pomocí `LIBNAME`, dotazujte se na ně přes
**Cypher/GQL**, spouštějte grafové **algoritmy**, kreslete **interaktivní
síťové diagramy** a stále používejte procedury pro síťovou optimalizaci a
analýzu **kompatibilní se SAS** — vše v jednom programu.

Toto úložiště ukazuje celý stack, ukotvený reálným vlajkovým notebookem a
vizualizačním demem bez databáze. Vše je poskytováno v **15 jazycích**
(viz [Jazyky](#jazyky)).

## Schopnosti

### Novinka — grafová rodina Jenneru (bez ekvivalentu v SAS)

| Funkce | Co dělá |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (nebo `MEMGRAPH`) | Naváže grafovou databázi na libref, jako každou jinou knihovnu. |
| **`PROC GQL`** | Spustí dotazy **Cypher / GQL** proti grafu a zapíše výslednou sadu do datové sady Jenner. |
| **`PROC LINKS`** | Spustí grafové **algoritmy** — PageRank, detekci komunit, nejkratší cestu, centralitu — proti grafu a zapíše výsledky za jednotlivé uzly / hrany do datové sady. |
| **`PROC NETVIZ`** | Vykreslí graf jako **interaktivní síťový diagram Cytoscape.js** (inline v kernelu Jupyter nebo jako samostatný soubor HTML z CLI). |

### Síťové procedury kompatibilní se SAS

| Funkce | Co dělá |
|---|---|
| **`PROC OPTNET`** | Síťová **optimalizace** nad datovými sadami Jenner — nejkratší cesta, TSP, tok s minimálními náklady, komponenty souvislosti, cykly, kliky a další. Port SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Klasická síťová **analýza** nad datovými sadami Jenner — centrality, komunity, biconnected komponenty, cesty. Port SAS Viya PROC NETWORK. |

Nová rodina pracuje nad **živou grafovou databází**; procedury kompatibilní
se SAS pracují nad **datovými sadami hran/uzlů**, které již máte. Skládají
se dohromady: stáhněte podgraf pomocí `PROC GQL`, ohodnoťte jej pomocí
`PROC LINKS` nebo `PROC NETWORK`, optimalizujte pomocí `PROC OPTNET` a
nakreslete jej pomocí `PROC NETVIZ`.

## Vlajkový notebook — analýza podvodů nad ICIJ offshore-leaks

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
spouští kompletní analytickou pipeline pro odhalování podvodů nad reálným
únikem **ICIJ Paradise Papers** (163 435 uzlů — offshore subjekty,
funkcionáři, adresy a zprostředkovatelé). Připojuje se pomocí
`LIBNAME … GRAPH ENGINE=NEO4J`, prozkoumává pomocí `PROC GQL` a hodnotí
riziko pomocí `PROC NETWORK` — kompletní, databází podložený grafový
workflow.

> Notebook se připojuje ke grafu Neo4j (platforma Jenner Workspace hostuje
> datovou sadu ICIJ). Nasměrujte `LIBNAME` na vlastní Neo4j/Memgraph a
> spusťte jej nad svými daty.

## Vizualizační demo — bez databáze

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) vykreslí
graf offshore vlastnictví jako interaktivní síťový diagram z prostých
datových sad — spusťte jej pouze pomocí CLI `jenner`:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Síťový diagram PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Požadavky

- Binárka `jenner` ve vaší proměnné `PATH`.
- Pro grafovou rodinu (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`):
  dosažitelná instance **Neo4j** nebo **Memgraph** a `jenner` sestavený s
  funkcí `neo4j`.
- Demo `PROC NETVIZ` a procedury kompatibilní se SAS žádnou databázi
  nepotřebují.

## Rozvržení

```
notebooks/en/   vlajkový notebook ICIJ (anglicky)
demos/          netviz_showcase — demo síťového diagramu bez databáze
i18n/<lang>/    lokalizovaný README + notebook pro jednotlivé jazyky
```

## Jazyky

Kompletní seznam dostupných jazyků najdete v hlavním souboru
[README](../../README.md). Každá jazyková složka obsahuje lokalizovaný
README a přeložený notebook.

## Licence

MIT. Data ICIJ jsou © ICIJ a používají se podle jejich podmínek; viz
notebook.
