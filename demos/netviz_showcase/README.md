# PROC NETVIZ showcase — network diagrams

`PROC NETVIZ` renders a graph as an **interactive Cytoscape.js** network
diagram. In the Jenner Jupyter kernel it displays inline; from the CLI it
writes a self-contained HTML file you open in any browser.

This demo needs **no database** — it builds a small offshore-ownership graph
from plain node/edge datasets and renders it, styled by role and connection
count.

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html  (open in a browser)
```

Example output (a PROC NETVIZ diagram):

![PROC NETVIZ network diagram](images/example_netviz.png)

PROC NETVIZ can also visualize a **live graph** — pass a `CONN=` graph libref
(Neo4j / Memgraph) or the result of a `PROC GQL` query instead of local
datasets. See the [ICIJ notebook](../../notebooks/en/icij_fraud_analytics.ipynb)
for the database-backed workflow.
