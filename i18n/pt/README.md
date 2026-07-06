# Neo4j e análise de redes com o Jenner

O [Jenner](https://jenneranalytics.com) traz bancos de dados de grafos e análise
de redes para o mundo do DATA step e dos PROCs compatível com SAS. Conecte-se ao **Neo4j**
ou ao **Memgraph** com um `LIBNAME`, consulte-os com **Cypher/GQL**, execute
**algoritmos** de grafo, desenhe **diagramas de rede interativos** e ainda use os
procedimentos de otimização e análise de redes **compatíveis com SAS** — tudo em um
único programa.

Este repositório mostra toda a pilha, ancorada por um notebook principal
do mundo real e uma demonstração de visualização sem banco de dados. Tudo é fornecido em
**15 idiomas** (veja [Idiomas](#idiomas)).

## Capacidades

### Novidade — a família de grafos do Jenner (sem equivalente no SAS)

| Recurso | O que faz |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (ou `MEMGRAPH`) | Vincula um banco de dados de grafos a um libref, como qualquer outra biblioteca. |
| **`PROC GQL`** | Executa consultas **Cypher / GQL** contra o grafo e grava o conjunto de resultados em um dataset do Jenner. |
| **`PROC LINKS`** | Executa **algoritmos** de grafo — PageRank, detecção de comunidades, caminho mais curto, centralidade — contra o grafo, gravando resultados por nó / por aresta em um dataset. |
| **`PROC NETVIZ`** | Renderiza um grafo como um diagrama de rede **interativo com Cytoscape.js** (inline no kernel do Jupyter, ou um arquivo HTML autocontido a partir da CLI). |

### Procedimentos de rede compatíveis com SAS

| Recurso | O que faz |
|---|---|
| **`PROC OPTNET`** | **Otimização** de redes sobre datasets do Jenner — caminho mais curto, TSP, fluxo de custo mínimo, componentes conexos, ciclos, cliques e mais. Uma portabilidade do PROC OPTNET do SAS/OR. |
| **`PROC NETWORK`** | **Análise** clássica de redes sobre datasets do Jenner — centralidades, comunidades, componentes biconexos, caminhos. Uma portabilidade do PROC NETWORK do SAS Viya. |

A nova família funciona sobre um **banco de dados de grafos ativo**; os procedimentos
compatíveis com SAS funcionam sobre **datasets de arestas/nós** que você já possui. Eles se compõem:
extraia um subgrafo com o `PROC GQL`, pontue-o com o `PROC LINKS` ou o `PROC NETWORK`,
otimize com o `PROC OPTNET` e desenhe-o com o `PROC NETVIZ`.

## Notebook principal — análise de fraude nos vazamentos offshore da ICIJ

O [`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
executa um pipeline completo de análise de fraude sobre o vazamento real dos **Paradise
Papers da ICIJ** (163.435 nós — entidades offshore, dirigentes, endereços e
intermediários). Ele se conecta com `LIBNAME … GRAPH ENGINE=NEO4J`, explora com
`PROC GQL` e pontua o risco com `PROC NETWORK` — um fluxo de trabalho de grafo
completo e respaldado por banco de dados.

> O notebook se conecta a um grafo Neo4j (a plataforma Jenner Workspace hospeda
> o dataset da ICIJ). Aponte o `LIBNAME` para o seu próprio Neo4j/Memgraph para executá-lo
> contra os seus dados.

## Demonstração de visualização — sem banco de dados

O [`demos/netviz_showcase/`](../../demos/netviz_showcase/) renderiza um grafo de
propriedade offshore como um diagrama de rede interativo a partir de datasets simples — execute-o
apenas com a CLI `jenner`:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![Diagrama de rede do PROC NETVIZ](../../demos/netviz_showcase/images/example_netviz.png)

## Requisitos

- O binário `jenner` no seu `PATH`.
- Para a família de grafos (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): uma instância
  **Neo4j** ou **Memgraph** acessível, e um `jenner` compilado com o recurso
  `neo4j`.
- A demonstração do `PROC NETVIZ` e os procedimentos compatíveis com SAS não precisam de banco de dados.

## Estrutura

```
notebooks/en/   o notebook principal da ICIJ (em inglês)
demos/          netviz_showcase — demonstração de diagrama de rede sem banco de dados
i18n/<lang>/    README + notebook localizados por idioma
```

## Idiomas

Cada pasta de idioma tem um README localizado e um notebook traduzido:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Licença

MIT. Os dados da ICIJ são © ICIJ e usados sob seus termos; veja o notebook.
