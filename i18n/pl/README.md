# Neo4j i analiza sieci z Jenner

[Jenner](https://jenneranalytics.com) wnosi grafowe bazy danych i
analizę sieci do świata kroku DATA i procedur PROC zgodnego z SAS.
Połącz się z **Neo4j** lub **Memgraph** za pomocą `LIBNAME`, odpytuj je
w **Cypher/GQL**, uruchamiaj **algorytmy** grafowe, rysuj
**interaktywne diagramy sieci** i wciąż korzystaj ze **zgodnych z SAS**
procedur optymalizacji i analizy sieci — wszystko w jednym programie.

To repozytorium pokazuje cały stos, oparty na flagowym notatniku z
rzeczywistego świata oraz demonstracji wizualizacji niewymagającej
bazy danych. Wszystko dostępne jest w **15 językach** (zobacz
[Języki](#języki)).

## Możliwości

### Nowość — grafowa rodzina Jenner (brak odpowiednika w SAS)

| Funkcja | Co robi |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (lub `MEMGRAPH`) | Wiąże grafową bazę danych z librefem, jak każdą inną bibliotekę. |
| **`PROC GQL`** | Uruchamia zapytania **Cypher / GQL** względem grafu i zapisuje zbiór wynikowy do zbioru danych Jenner. |
| **`PROC LINKS`** | Uruchamia **algorytmy** grafowe — PageRank, wykrywanie społeczności, najkrótszą ścieżkę, centralność — względem grafu, zapisując wyniki per węzeł / per krawędź do zbioru danych. |
| **`PROC NETVIZ`** | Renderuje graf jako **interaktywny diagram sieci Cytoscape.js** (osadzony w jądrze Jupyter lub jako samodzielny plik HTML z poziomu CLI). |

### Procedury sieciowe zgodne z SAS

| Funkcja | Co robi |
|---|---|
| **`PROC OPTNET`** | **Optymalizacja** sieci na zbiorach danych Jenner — najkrótsza ścieżka, TSP, przepływ o minimalnym koszcie, spójne składowe, cykle, kliki i więcej. Port PROC OPTNET z SAS/OR. |
| **`PROC NETWORK`** | Klasyczna **analiza** sieci na zbiorach danych Jenner — centralności, społeczności, składowe dwuspójne, ścieżki. Port PROC NETWORK z SAS Viya. |

Nowa rodzina działa na **żywej grafowej bazie danych**; procedury
zgodne z SAS działają na posiadanych już zbiorach danych
krawędzi/węzłów. Komponują się ze sobą: pobierz podgraf za pomocą
`PROC GQL`, oceń go z `PROC LINKS` lub `PROC NETWORK`, zoptymalizuj z
`PROC OPTNET` i narysuj z `PROC NETVIZ`.

## Flagowy notatnik — analiza nadużyć na wycieku offshore ICIJ

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb) uruchamia
kompleksowy potok analityki nadużyć na **prawdziwym wycieku ICIJ
Paradise Papers** (163,435 węzłów — podmioty offshore, członkowie
kierownictwa, adresy i pośrednicy). Łączy się za pomocą
`LIBNAME … GRAPH ENGINE=NEO4J`, eksploruje z `PROC GQL` i ocenia ryzyko
z `PROC NETWORK` — kompletny, oparty na bazie danych przepływ pracy
grafowej.

> Notatnik łączy się z grafem Neo4j (platforma Jenner Workspace hostuje
> zbiór danych ICIJ). Skieruj `LIBNAME` na własny Neo4j/Memgraph, aby
> uruchomić go na swoich danych.

## Demonstracja wizualizacji — bez bazy danych

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/)
renderuje graf własności offshore jako interaktywny diagram sieci ze
zwykłych zbiorów danych — uruchom go z użyciem samego CLI `jenner`:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Diagram sieci PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Wymagania

- Plik binarny `jenner` na Twojej ścieżce `PATH`.
- Dla rodziny grafowej (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`):
  osiągalna instancja **Neo4j** lub **Memgraph** oraz `jenner`
  zbudowany z funkcją `neo4j`.
- Demonstracja `PROC NETVIZ` i procedury zgodne z SAS nie wymagają
  bazy danych.

## Układ

```
notebooks/en/   flagowy notatnik ICIJ (angielski)
demos/          netviz_showcase — demo diagramu sieci bez bazy danych
i18n/<lang>/    zlokalizowany README + notatnik dla każdego języka
```

## Języki

Każdy folder językowy zawiera zlokalizowany README oraz przetłumaczony
notatnik:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Licencja

MIT. Dane ICIJ są © ICIJ i używane na ich warunkach; zobacz notatnik.
