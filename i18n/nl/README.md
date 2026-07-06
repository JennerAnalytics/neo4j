# Neo4j & netwerkanalyse met Jenner

[Jenner](https://jenneranalytics.com) brengt grafendatabases en
netwerkanalyse naar de SAS-compatibele DATA-stap en PROC-wereld. Verbind
met **Neo4j** of **Memgraph** via een `LIBNAME`, bevraag ze met
**Cypher/GQL**, draai graaf**algoritmen**, teken **interactieve
netwerkdiagrammen**, en gebruik daarnaast nog steeds de
**SAS-compatibele** procedures voor netwerkoptimalisatie en -analyse —
allemaal in één programma.

Deze repository toont de volledige stack, verankerd door een
vlaggenschip-notebook uit de praktijk en een visualisatiedemo zonder
database. Alles wordt aangeboden in **15 talen** (zie
[Talen](#talen)).

## Mogelijkheden

### Nieuw — de grafenfamilie van Jenner (geen SAS-equivalent)

| Functie | Wat het doet |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (of `MEMGRAPH`) | Koppel een grafendatabase aan een libref, net als elke andere bibliotheek. |
| **`PROC GQL`** | Voer **Cypher-/GQL**-query's uit tegen de graaf en schrijf de resultatenset naar een Jenner-dataset. |
| **`PROC LINKS`** | Draai graaf**algoritmen** — PageRank, gemeenschapsdetectie, kortste pad, centraliteit — tegen de graaf en schrijf resultaten per knoop/rand naar een dataset. |
| **`PROC NETVIZ`** | Render een graaf als een **interactief Cytoscape.js**-netwerkdiagram (inline in de Jupyter-kernel, of als zelfstandig HTML-bestand vanaf de CLI). |

### SAS-compatibele netwerkprocedures

| Functie | Wat het doet |
|---|---|
| **`PROC OPTNET`** | Netwerk**optimalisatie** over Jenner-datasets — kortste pad, TSP, minimum-kostenstroom, verbonden componenten, cykels, cliques en meer. Een port van SAS/OR PROC OPTNET. |
| **`PROC NETWORK`** | Klassieke netwerk**analyse** over Jenner-datasets — centraliteiten, gemeenschappen, biconnecte componenten, paden. Een port van SAS Viya PROC NETWORK. |

De nieuwe familie werkt op een **live grafendatabase**; de
SAS-compatibele procedures werken op **links-/knopen-datasets** die je
al hebt. Ze zijn combineerbaar: haal een subgraaf op met `PROC GQL`,
scoor die met `PROC LINKS` of `PROC NETWORK`, optimaliseer met
`PROC OPTNET`, en teken hem met `PROC NETVIZ`.

## Vlaggenschip-notebook — ICIJ offshore-leaks-fraudeanalyse

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
draait een volledige fraudeanalyse-pijplijn tegen het **echte ICIJ
Paradise Papers**-lek (163.435 knopen — offshore-entiteiten,
functionarissen, adressen en tussenpersonen). Het verbindt met
`LIBNAME … GRAPH ENGINE=NEO4J`, verkent met `PROC GQL`, en scoort
risico met `PROC NETWORK` — een complete, database-ondersteunde
grafenworkflow.

> De notebook verbindt met een Neo4j-graaf (het Jenner
> Workspace-platform host de ICIJ-dataset). Richt de `LIBNAME` op je
> eigen Neo4j/Memgraph om hem tegen je eigen gegevens te draaien.

## Visualisatiedemo — geen database vereist

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) rendert
een graaf van offshore-eigendom als een interactief netwerkdiagram uit
gewone datasets — draai het met alleen de `jenner`-CLI:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ-netwerkdiagram](../../demos/netviz_showcase/images/example_netviz.png)

## Vereisten

- Het `jenner`-binary op je `PATH`.
- Voor de grafenfamilie (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`):
  een bereikbare **Neo4j**- of **Memgraph**-instantie, en een `jenner`
  gebouwd met de `neo4j`-feature.
- De `PROC NETVIZ`-demo en de SAS-compatibele procedures hebben geen
  database nodig.

## Indeling

```
notebooks/en/   het vlaggenschip-ICIJ-notebook (Engels)
demos/          netviz_showcase — netwerkdiagram-demo zonder database
i18n/<taal>/    gelokaliseerde README + notebook per taal
```

## Talen

Elke taalmap bevat een gelokaliseerde README en een vertaalde notebook.
Zie de [volledige talenlijst in de hoofd-README](../../README.md).

## Licentie

MIT. De ICIJ-gegevens zijn © ICIJ en worden gebruikt onder hun
voorwaarden; zie de notebook.
