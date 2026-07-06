# Neo4j et analyse de réseaux avec Jenner

[Jenner](https://jenneranalytics.com) apporte les bases de données de
graphes et l'analyse de réseaux dans l'univers de l'étape DATA et des
PROC compatibles SAS. Connectez-vous à **Neo4j** ou **Memgraph** avec
un `LIBNAME`, interrogez-les en **Cypher/GQL**, exécutez des
**algorithmes** de graphe, tracez des **diagrammes de réseau
interactifs** et utilisez toujours les procédures d'analyse et
d'optimisation de réseaux **compatibles SAS** — le tout dans un seul
programme.

Ce dépôt présente l'ensemble de la pile, articulé autour d'un notebook
phare inspiré du monde réel et d'une démonstration de visualisation
sans base de données. Tout est fourni en **15 langues** (voir
[Langues](#langues)).

## Fonctionnalités

### Nouveau — la famille graphe de Jenner (sans équivalent SAS)

| Fonctionnalité | Ce qu'elle fait |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (ou `MEMGRAPH`) | Rattache une base de données de graphes à un libref, comme n'importe quelle autre bibliothèque. |
| **`PROC GQL`** | Exécute des requêtes **Cypher / GQL** contre le graphe et écrit l'ensemble de résultats dans un jeu de données Jenner. |
| **`PROC LINKS`** | Exécute des **algorithmes** de graphe — PageRank, détection de communautés, plus court chemin, centralité — contre le graphe, en écrivant les résultats par nœud / par arête dans un jeu de données. |
| **`PROC NETVIZ`** | Rend un graphe sous forme de diagramme de réseau **Cytoscape.js interactif** (en ligne dans le noyau Jupyter, ou sous forme de fichier HTML autonome depuis la CLI). |

### Procédures de réseau compatibles SAS

| Fonctionnalité | Ce qu'elle fait |
|---|---|
| **`PROC OPTNET`** | **Optimisation** de réseau sur des jeux de données Jenner — plus court chemin, TSP, flot à coût minimal, composantes connexes, cycles, cliques, et plus encore. Un portage de PROC OPTNET de SAS/OR. |
| **`PROC NETWORK`** | **Analyse** de réseau classique sur des jeux de données Jenner — centralités, communautés, composantes biconnexes, chemins. Un portage de PROC NETWORK de SAS Viya. |

La nouvelle famille travaille sur une **base de données de graphes en
direct** ; les procédures compatibles SAS travaillent sur des jeux de
données **liens/nœuds** que vous possédez déjà. Elles se composent :
extrayez un sous-graphe avec `PROC GQL`, notez-le avec `PROC LINKS` ou
`PROC NETWORK`, optimisez avec `PROC OPTNET`, et tracez-le avec
`PROC NETVIZ`.

## Notebook phare — analyse anti-fraude des fuites offshore de l'ICIJ

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb) exécute une
chaîne complète d'analyse anti-fraude sur la fuite réelle des **Paradise
Papers de l'ICIJ** (163 435 nœuds — entités offshore, dirigeants,
adresses et intermédiaires). Il se connecte avec
`LIBNAME … GRAPH ENGINE=NEO4J`, explore avec `PROC GQL` et évalue le
risque avec `PROC NETWORK` — un flux de travail de graphe complet,
adossé à une base de données.

> Le notebook se connecte à un graphe Neo4j (la plateforme Jenner
> Workspace héberge le jeu de données de l'ICIJ). Pointez le `LIBNAME`
> vers votre propre Neo4j/Memgraph pour l'exécuter sur vos données.

## Démonstration de visualisation — aucune base de données requise

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) rend un
graphe de propriété offshore sous forme de diagramme de réseau
interactif à partir de simples jeux de données — exécutez-le avec la
seule CLI `jenner` :

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Diagramme de réseau PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Prérequis

- Le binaire `jenner` sur votre `PATH`.
- Pour la famille graphe (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`) :
  une instance **Neo4j** ou **Memgraph** joignable, et un `jenner`
  compilé avec la fonctionnalité `neo4j`.
- La démonstration `PROC NETVIZ` et les procédures compatibles SAS ne
  nécessitent aucune base de données.

## Organisation

```
notebooks/en/   le notebook phare ICIJ (anglais)
demos/          netviz_showcase — démonstration de diagramme de réseau sans base de données
i18n/<lang>/    README localisé + notebook par langue
```

## Langues

Chaque dossier de langue contient un README localisé et un notebook
traduit : voir le [README principal](../../README.md) pour la liste
complète des langues.

## Licence

MIT. Les données de l'ICIJ sont © ICIJ et utilisées selon leurs
conditions ; voir le notebook.
