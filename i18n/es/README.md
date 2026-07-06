# Neo4j y análisis de redes con Jenner

[Jenner](https://jenneranalytics.com) lleva las bases de datos de grafos y el
análisis de redes al mundo del paso DATA y los PROC compatibles con SAS.
Conéctate a **Neo4j** o **Memgraph** con un `LIBNAME`, consúltalos con
**Cypher/GQL**, ejecuta **algoritmos** de grafos, dibuja **diagramas de red
interactivos** y sigue usando los procedimientos de optimización y análisis de
redes **compatibles con SAS** — todo en un mismo programa.

Este repositorio muestra la pila completa, anclada en un cuaderno insignia
basado en un caso real y en una demostración de visualización sin base de
datos. Todo se ofrece en **15 idiomas** (consulta [Idiomas](#idiomas)).

## Capacidades

### Nuevo — la familia de grafos de Jenner (sin equivalente en SAS)

| Función | Qué hace |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (o `MEMGRAPH`) | Vincula una base de datos de grafos a un libref, como cualquier otra biblioteca. |
| **`PROC GQL`** | Ejecuta consultas **Cypher / GQL** sobre el grafo y escribe el conjunto de resultados en un conjunto de datos de Jenner. |
| **`PROC LINKS`** | Ejecuta **algoritmos** de grafos — PageRank, detección de comunidades, camino más corto, centralidad — sobre el grafo, escribiendo resultados por nodo / por arista en un conjunto de datos. |
| **`PROC NETVIZ`** | Representa un grafo como un diagrama de red **interactivo con Cytoscape.js** (en línea en el kernel de Jupyter, o como un archivo HTML autónomo desde la CLI). |

### Procedimientos de red compatibles con SAS

| Función | Qué hace |
|---|---|
| **`PROC OPTNET`** | **Optimización** de redes sobre conjuntos de datos de Jenner — camino más corto, TSP, flujo de coste mínimo, componentes conexos, ciclos, clanes y más. Una adaptación de PROC OPTNET de SAS/OR. |
| **`PROC NETWORK`** | **Análisis** clásico de redes sobre conjuntos de datos de Jenner — centralidades, comunidades, componentes biconexos, caminos. Una adaptación de PROC NETWORK de SAS Viya. |

La nueva familia trabaja sobre una **base de datos de grafos en vivo**; los
procedimientos compatibles con SAS trabajan sobre conjuntos de datos de
**enlaces/nodos** que ya tengas. Se combinan entre sí: extrae un subgrafo con
`PROC GQL`, puntúalo con `PROC LINKS` o `PROC NETWORK`, optimízalo con
`PROC OPTNET` y dibújalo con `PROC NETVIZ`.

## Cuaderno insignia — análisis de fraude de los Offshore Leaks del ICIJ

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb) ejecuta una
canalización integral de análisis de fraude contra la filtración real de los
**Paradise Papers del ICIJ** (163,435 nodos — entidades extraterritoriales,
directivos, direcciones e intermediarios). Se conecta con
`LIBNAME … GRAPH ENGINE=NEO4J`, explora con `PROC GQL` y puntúa el riesgo con
`PROC NETWORK` — un flujo de trabajo de grafos completo respaldado por una base
de datos.

> El cuaderno se conecta a un grafo de Neo4j (la plataforma Jenner Workspace
> aloja el conjunto de datos del ICIJ). Apunta el `LIBNAME` a tu propio
> Neo4j/Memgraph para ejecutarlo contra tus datos.

## Demostración de visualización — sin base de datos

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) representa un
grafo de propiedad extraterritorial como un diagrama de red interactivo a
partir de conjuntos de datos simples — ejecútalo con solo la CLI `jenner`:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Diagrama de red de PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Requisitos

- El binario `jenner` en tu `PATH`.
- Para la familia de grafos (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): una
  instancia de **Neo4j** o **Memgraph** accesible, y un `jenner` compilado con
  la característica `neo4j`.
- La demostración de `PROC NETVIZ` y los procedimientos compatibles con SAS no
  necesitan base de datos.

## Estructura

```
notebooks/en/   el cuaderno insignia del ICIJ (inglés)
demos/          netviz_showcase — demostración de diagrama de red sin base de datos
i18n/<lang>/    README + cuaderno localizados por idioma
```

## Idiomas

Cada carpeta de idioma tiene un README localizado y un cuaderno traducido:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Licencia

MIT. Los datos del ICIJ son © ICIJ y se usan bajo sus términos; consulta el
cuaderno.
