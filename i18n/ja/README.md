# Jenner によるグラフデータベースとネットワーク分析

[Jenner](https://jenneranalytics.com) は、グラフデータベースとネットワーク
分析を、SAS 互換の DATA ステップと PROC の世界に取り込みます。**Neo4j** や
**Memgraph** に `LIBNAME` で接続し、**Cypher/GQL** でクエリを実行し、グラフ
**アルゴリズム** を走らせ、**インタラクティブなネットワーク図** を描き、
さらに **SAS 互換** のネットワーク最適化・分析プロシージャも使えます。
これらすべてが 1 つのプログラムの中で完結します。

このリポジトリは、実世界のフラッグシップ・ノートブックと、データベース
不要の可視化デモを軸に、スタック全体を紹介します。すべては **15 言語**
で提供されています（[言語](#言語) を参照)。

## 機能

### 新機能 — Jenner のグラフファミリー（SAS に相当機能なし)

| 機能 | 内容 |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`**（または `MEMGRAPH`) | 他のライブラリと同じように、グラフデータベースを libref に結び付けます。 |
| **`PROC GQL`** | グラフに対して **Cypher / GQL** クエリを実行し、結果セットを Jenner データセットに書き出します。 |
| **`PROC LINKS`** | グラフに対してグラフ **アルゴリズム**（PageRank、コミュニティ検出、最短経路、中心性）を実行し、ノード単位／辺単位の結果をデータセットに書き出します。 |
| **`PROC NETVIZ`** | グラフを **インタラクティブな Cytoscape.js** ネットワーク図として描画します（Jupyter カーネル内にインライン表示、または CLI から自己完結型の HTML ファイルとして出力)。 |

### SAS 互換のネットワークプロシージャ

| 機能 | 内容 |
|---|---|
| **`PROC OPTNET`** | Jenner データセットに対するネットワーク **最適化** — 最短経路、TSP、最小費用流、連結成分、閉路、クリークなど。SAS/OR PROC OPTNET の移植版です。 |
| **`PROC NETWORK`** | Jenner データセットに対する古典的なネットワーク **分析** — 中心性、コミュニティ、二連結成分、経路。SAS Viya PROC NETWORK の移植版です。 |

新しいファミリーは **ライブのグラフデータベース** 上で動作し、SAS 互換の
プロシージャは、すでに手元にある **辺／ノードのデータセット** 上で動作
します。これらは組み合わせられます。すなわち `PROC GQL` でサブグラフを
取得し、`PROC LINKS` または `PROC NETWORK` でスコアリングし、`PROC OPTNET`
で最適化し、`PROC NETVIZ` で描画します。

## フラッグシップ・ノートブック — ICIJ オフショアリークの不正分析

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
は、実際の **ICIJ パラダイス文書**（Paradise Papers）のリーク（163,435
ノード — オフショア法人、役員、住所、仲介者)に対して、エンドツーエンドの
不正分析パイプラインを実行します。`LIBNAME … GRAPH ENGINE=NEO4J` で接続し、
`PROC GQL` で探索し、`PROC NETWORK` でリスクをスコアリングする、完結した
データベース駆動のグラフワークフローです。

> このノートブックは Neo4j グラフに接続します（Jenner Workspace
> プラットフォームが ICIJ データセットをホストしています)。`LIBNAME` を
> ご自身の Neo4j/Memgraph に向ければ、自分のデータに対して実行できます。

## 可視化デモ — データベース不要

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) は、プレーンな
データセットからオフショア所有グラフをインタラクティブなネットワーク図
として描画します。`jenner` CLI だけで実行できます。

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ ネットワーク図](../../demos/netviz_showcase/images/example_netviz.png)

## 要件

- `PATH` 上に `jenner` バイナリがあること。
- グラフファミリー（`LIBNAME GRAPH`、`PROC GQL`、`PROC LINKS`)には、到達
  可能な **Neo4j** または **Memgraph** インスタンスと、`neo4j` フィーチャ付き
  でビルドした `jenner` が必要です。
- `PROC NETVIZ` のデモと SAS 互換プロシージャにはデータベースは不要です。

## 構成

```
notebooks/en/   フラッグシップの ICIJ ノートブック（英語）
demos/          netviz_showcase — データベース不要のネットワーク図デモ
i18n/<lang>/    言語ごとのローカライズ済み README + ノートブック
```

## 言語

各言語フォルダーには、ローカライズ済みの README と翻訳されたノートブックが
あります。

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## ライセンス

MIT。ICIJ データは © ICIJ であり、同団体の規約に基づいて使用しています。
詳細はノートブックを参照してください。
