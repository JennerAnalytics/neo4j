# Neo4j und Netzwerkanalyse mit Jenner

[Jenner](https://jenneranalytics.com) bringt Graphdatenbanken und
Netzwerkanalyse in die SAS-kompatible Welt aus DATA-Schritt und PROC.
Verbinden Sie sich mit **Neo4j** oder **Memgraph** über ein `LIBNAME`,
fragen Sie sie mit **Cypher/GQL** ab, führen Sie Graph-**Algorithmen**
aus, zeichnen Sie **interaktive Netzwerkdiagramme** und nutzen Sie
weiterhin die **SAS-kompatiblen** Prozeduren zur Netzwerkoptimierung
und -analyse — alles in einem einzigen Programm.

Dieses Repository zeigt den gesamten Stack, verankert in einem
praxisnahen Vorzeige-Notebook und einer Visualisierungs-Demo ohne
Datenbank. Alles wird in **15 Sprachen** bereitgestellt (siehe
[Sprachen](#sprachen)).

## Funktionen

### Neu — Jenners Graph-Familie (kein SAS-Äquivalent)

| Funktion | Was sie leistet |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (oder `MEMGRAPH`) | Bindet eine Graphdatenbank an ein Libref, wie jede andere Bibliothek. |
| **`PROC GQL`** | Führt **Cypher-/GQL**-Abfragen gegen den Graphen aus und schreibt die Ergebnismenge in einen Jenner-Datensatz. |
| **`PROC LINKS`** | Führt Graph-**Algorithmen** aus — PageRank, Community-Erkennung, kürzester Pfad, Zentralität — gegen den Graphen und schreibt Ergebnisse je Knoten/Kante in einen Datensatz. |
| **`PROC NETVIZ`** | Rendert einen Graphen als **interaktives Cytoscape.js**-Netzwerkdiagramm (inline im Jupyter-Kernel oder als eigenständige HTML-Datei über die CLI). |

### SAS-kompatible Netzwerkprozeduren

| Funktion | Was sie leistet |
|---|---|
| **`PROC OPTNET`** | Netzwerk-**Optimierung** über Jenner-Datensätze — kürzester Pfad, TSP, kostenminimaler Fluss, Zusammenhangskomponenten, Zyklen, Cliquen und mehr. Eine Portierung von SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Klassische Netzwerk-**Analyse** über Jenner-Datensätze — Zentralitäten, Communitys, biconnected components, Pfade. Eine Portierung von SAS Viya PROC NETWORK. |

Die neue Familie arbeitet auf einer **Live-Graphdatenbank**; die
SAS-kompatiblen Prozeduren arbeiten auf **Kanten-/Knoten-Datensätzen**,
die Sie bereits besitzen. Sie lassen sich kombinieren: Ziehen Sie
einen Teilgraphen mit `PROC GQL`, bewerten Sie ihn mit `PROC LINKS`
oder `PROC NETWORK`, optimieren Sie mit `PROC OPTNET` und zeichnen Sie
ihn mit `PROC NETVIZ`.

## Vorzeige-Notebook — Betrugsanalyse der ICIJ-Offshore-Leaks

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
führt eine durchgängige Betrugsanalyse-Pipeline gegen das echte
**ICIJ-Paradise-Papers**-Leak aus (163.435 Knoten —
Offshore-Entitäten, Amtsträger, Adressen und Intermediäre). Es
verbindet sich mit `LIBNAME … GRAPH ENGINE=NEO4J`, erkundet mit
`PROC GQL` und bewertet Risiko mit `PROC NETWORK` — ein vollständiger,
datenbankgestützter Graph-Workflow.

> Das Notebook verbindet sich mit einem Neo4j-Graphen (die
> Jenner-Workspace-Plattform hostet den ICIJ-Datensatz). Richten Sie
> das `LIBNAME` auf Ihr eigenes Neo4j/Memgraph, um es gegen Ihre
> Daten auszuführen.

## Visualisierungs-Demo — keine Datenbank erforderlich

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) rendert
einen Offshore-Eigentümergraphen als interaktives Netzwerkdiagramm aus
einfachen Datensätzen — führen Sie es allein mit der `jenner`-CLI aus:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ Netzwerkdiagramm](../../demos/netviz_showcase/images/example_netviz.png)

## Voraussetzungen

- Die `jenner`-Binärdatei auf Ihrem `PATH`.
- Für die Graph-Familie (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`):
  eine erreichbare **Neo4j**- oder **Memgraph**-Instanz und ein
  `jenner`, das mit dem `neo4j`-Feature gebaut wurde.
- Die `PROC NETVIZ`-Demo und die SAS-kompatiblen Prozeduren benötigen
  keine Datenbank.

## Aufbau

```
notebooks/en/   das Vorzeige-ICIJ-Notebook (Englisch)
demos/          netviz_showcase — Netzwerkdiagramm-Demo ohne Datenbank
i18n/<lang>/    lokalisierte README + Notebook je Sprache
```

## Sprachen

Dieses Repository ist in 15 Sprachen verfügbar. Siehe die
[Sprachtabelle in der Haupt-README](../../README.md) für alle
Übersetzungen.

## Lizenz

MIT. Die ICIJ-Daten sind © ICIJ und werden unter deren Bedingungen
verwendet; siehe das Notebook.
