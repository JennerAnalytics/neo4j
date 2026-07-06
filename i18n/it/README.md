# Neo4j e analisi di rete con Jenner

[Jenner](https://jenneranalytics.com) porta i database a grafo e
l'analisi di rete nel mondo del DATA step e delle PROC compatibili con
SAS. Connettiti a **Neo4j** o **Memgraph** con un `LIBNAME`, interrogali
con **Cypher/GQL**, esegui **algoritmi** di grafo, disegna **diagrammi
di rete interattivi** e usa comunque le procedure di **ottimizzazione e
analisi di rete compatibili con SAS** — tutto in un unico programma.

Questo repository mostra l'intero stack, ancorato a un notebook
faro tratto dal mondo reale e a una demo di visualizzazione senza
database. Tutto è fornito in **15 lingue** (vedi [Lingue](#lingue)).

## Funzionalità

### Novità — la famiglia grafo di Jenner (nessun equivalente SAS)

| Funzionalità | Cosa fa |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (o `MEMGRAPH`) | Associa un database a grafo a un libref, come qualsiasi altra libreria. |
| **`PROC GQL`** | Esegue query **Cypher / GQL** sul grafo e scrive l'insieme dei risultati in un dataset Jenner. |
| **`PROC LINKS`** | Esegue **algoritmi** di grafo — PageRank, rilevamento delle comunità, cammino minimo, centralità — sul grafo, scrivendo i risultati per nodo / per arco in un dataset. |
| **`PROC NETVIZ`** | Rende un grafo come un **diagramma di rete Cytoscape.js interattivo** (inline nel kernel Jupyter, o come file HTML autonomo dalla CLI). |

### Procedure di rete compatibili con SAS

| Funzionalità | Cosa fa |
|---|---|
| **`PROC OPTNET`** | **Ottimizzazione** di rete sui dataset Jenner — cammino minimo, TSP, flusso a costo minimo, componenti connesse, cicli, clique e altro. Un port di PROC OPTNET di SAS/OR. |
| **`PROC NETWORK`** | **Analisi** di rete classica sui dataset Jenner — centralità, comunità, componenti biconnesse, cammini. Un port di PROC NETWORK di SAS Viya. |

La nuova famiglia opera su un **database a grafo dal vivo**; le
procedure compatibili con SAS operano su **dataset di archi/nodi** che
possiedi già. Si compongono: estrai un sotto-grafo con `PROC GQL`,
assegnagli un punteggio con `PROC LINKS` o `PROC NETWORK`, ottimizza con
`PROC OPTNET` e disegnalo con `PROC NETVIZ`.

## Notebook faro — analisi antifrode sulle fughe offshore ICIJ

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
esegue una pipeline di analisi antifrode end-to-end sulla vera fuga di
dati **ICIJ Paradise Papers** (163.435 nodi — entità offshore,
funzionari, indirizzi e intermediari). Si connette con
`LIBNAME … GRAPH ENGINE=NEO4J`, esplora con `PROC GQL` e valuta il
rischio con `PROC NETWORK` — un flusso di lavoro completo su grafo,
supportato da un database.

> Il notebook si connette a un grafo Neo4j (la piattaforma Jenner
> Workspace ospita il dataset ICIJ). Punta il `LIBNAME` al tuo Neo4j/
> Memgraph per eseguirlo sui tuoi dati.

## Demo di visualizzazione — nessun database richiesto

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) rende un
grafo di proprietà offshore come un diagramma di rete interattivo a
partire da semplici dataset — eseguilo con la sola CLI `jenner`:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Diagramma di rete PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Requisiti

- Il binario `jenner` nel tuo `PATH`.
- Per la famiglia grafo (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): una
  istanza **Neo4j** o **Memgraph** raggiungibile, e un `jenner`
  compilato con la feature `neo4j`.
- La demo `PROC NETVIZ` e le procedure compatibili con SAS non
  richiedono alcun database.

## Struttura

```
notebooks/en/   il notebook ICIJ faro (inglese)
demos/          netviz_showcase — demo di diagramma di rete senza database
i18n/<lang>/    README + notebook localizzati per lingua
```

## Lingue

Ogni cartella di lingua ha un README localizzato e un notebook tradotto:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Licenza

MIT. I dati ICIJ sono © ICIJ e usati secondo i loro termini; vedi il
notebook.
