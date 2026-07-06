# Neo4j & network analysis with Jenner

[Jenner](https://jenneranalytics.com) brings graph databases and network
analysis into the SAS-compatible DATA step and PROC world. Connect to **Neo4j**
or **Memgraph** with a `LIBNAME`, query them with **Cypher/GQL**, run graph
**algorithms**, draw **interactive network diagrams**, and still use the
**SAS-compatible** network-optimization and analysis procedures — all in one
program.

This repository shows the whole stack, anchored by a real-world flagship
notebook and a no-database visualization demo. Everything is provided in
**15 languages** (see [Languages](#languages)).

## Capabilities

### New — Jenner's graph family (no SAS equivalent)

| Feature | What it does |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (or `MEMGRAPH`) | Bind a graph database to a libref, like any other library. |
| **`PROC GQL`** | Run **Cypher / GQL** queries against the graph and write the result set to a Jenner dataset. |
| **`PROC LINKS`** | Run graph **algorithms** — PageRank, community detection, shortest path, centrality — against the graph, writing per-node / per-edge results to a dataset. |
| **`PROC NETVIZ`** | Render a graph as an **interactive Cytoscape.js** network diagram (inline in the Jupyter kernel, or a self-contained HTML file from the CLI). |

### SAS-compatible network procedures

| Feature | What it does |
|---|---|
| **`PROC OPTNET`** | Network **optimization** over Jenner datasets — shortest path, TSP, minimum-cost flow, connected components, cycles, cliques, and more. A port of SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Classical network **analysis** over Jenner datasets — centralities, communities, biconnected components, paths. A port of SAS Viya PROC NETWORK. |

The new family works on a **live graph database**; the SAS-compatible
procedures work on **links/nodes datasets** you already have. They compose:
pull a subgraph with `PROC GQL`, score it with `PROC LINKS` or `PROC NETWORK`,
optimize with `PROC OPTNET`, and draw it with `PROC NETVIZ`.

## Flagship notebook — ICIJ offshore-leaks fraud analytics

[`notebooks/en/icij_fraud_analytics.ipynb`](notebooks/en/icij_fraud_analytics.ipynb)
runs an end-to-end fraud-analytics pipeline against the **real ICIJ Paradise
Papers** leak (163,435 nodes — offshore entities, officers, addresses, and
intermediaries). It connects with `LIBNAME … GRAPH ENGINE=NEO4J`, explores with
`PROC GQL`, and scores risk with `PROC NETWORK` — a complete, database-backed
graph workflow.

> The notebook connects to a Neo4j graph (the Jenner Workspace platform hosts
> the ICIJ dataset). Point the `LIBNAME` at your own Neo4j/Memgraph to run it
> against your data.

## Visualization demo — no database required

[`demos/netviz_showcase/`](demos/netviz_showcase/) renders an offshore-ownership
graph as an interactive network diagram from plain datasets — run it with just
the `jenner` CLI:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ network diagram](demos/netviz_showcase/images/example_netviz.png)

## Requirements

- The `jenner` binary on your `PATH`.
- For the graph family (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): a reachable
  **Neo4j** or **Memgraph** instance, and a `jenner` built with the `neo4j`
  feature.
- The `PROC NETVIZ` demo and the SAS-compatible procedures need no database.

## Layout

```
notebooks/en/   the flagship ICIJ notebook (English)
demos/          netviz_showcase — no-database network-diagram demo
i18n/<lang>/    localized README + notebook per language
```

## Languages

Each language folder has a localized README and a translated notebook:

| | | | |
|---|---|---|---|
| [Čeština](i18n/cs/README.md) | [Dansk](i18n/da/README.md) | [Deutsch](i18n/de/README.md) | [Ελληνικά](i18n/el/README.md) |
| [Español](i18n/es/README.md) | [Suomi](i18n/fi/README.md) | [Français](i18n/fr/README.md) | [Italiano](i18n/it/README.md) |
| [日本語](i18n/ja/README.md) | [한국어](i18n/ko/README.md) | [Nederlands](i18n/nl/README.md) | [Polski](i18n/pl/README.md) |
| [Português](i18n/pt/README.md) | [Svenska](i18n/sv/README.md) | [中文](i18n/zh/README.md) | |

## License

MIT. The ICIJ data is © ICIJ and used under their terms; see the notebook.
