# Neo4j와 네트워크 분석, Jenner로

[Jenner](https://jenneranalytics.com)는 그래프 데이터베이스와 네트워크
분석을 SAS 호환 DATA 스텝 및 PROC 세계로 가져온다. `LIBNAME`으로
**Neo4j** 또는 **Memgraph**에 연결하고, **Cypher/GQL**로 질의하며,
그래프 **알고리즘**을 실행하고, **대화형 네트워크 다이어그램**을
그리면서도, 여전히 **SAS 호환** 네트워크 최적화 및 분석 프로시저를
사용한다 — 이 모든 것을 하나의 프로그램에서.

이 저장소는 실전 대표 노트북과 데이터베이스가 필요 없는 시각화
데모를 중심으로 전체 스택을 보여준다. 모든 것은 **15개 언어**로
제공된다([언어](#언어) 참조).

## 기능

### 신규 — Jenner의 그래프 제품군 (SAS 대응물 없음)

| 기능 | 하는 일 |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (또는 `MEMGRAPH`) | 다른 라이브러리처럼 그래프 데이터베이스를 libref에 바인딩한다. |
| **`PROC GQL`** | 그래프에 대해 **Cypher / GQL** 쿼리를 실행하고 결과 집합을 Jenner 데이터셋에 기록한다. |
| **`PROC LINKS`** | 그래프에 대해 **알고리즘** — PageRank, 커뮤니티 탐지, 최단 경로, 중심성 — 을 실행하고 노드별/엣지별 결과를 데이터셋에 기록한다. |
| **`PROC NETVIZ`** | 그래프를 **대화형 Cytoscape.js** 네트워크 다이어그램으로 렌더링한다(Jupyter 커널 내 인라인, 또는 CLI에서 독립 실행형 HTML 파일). |

### SAS 호환 네트워크 프로시저

| 기능 | 하는 일 |
|---|---|
| **`PROC OPTNET`** | Jenner 데이터셋에 대한 네트워크 **최적화** — 최단 경로, TSP, 최소 비용 흐름, 연결 요소, 순환, 클리크 등. SAS/OR PROC OPTNET의 포팅. |
| **`PROC NETWORK`** | Jenner 데이터셋에 대한 고전적 네트워크 **분석** — 중심성, 커뮤니티, 이중 연결 요소, 경로. SAS Viya PROC NETWORK의 포팅. |

신규 제품군은 **라이브 그래프 데이터베이스**에서 동작하고, SAS
호환 프로시저는 이미 보유한 **링크/노드 데이터셋**에서 동작한다.
이들은 조합할 수 있다: `PROC GQL`로 하위 그래프를 가져오고,
`PROC LINKS` 또는 `PROC NETWORK`로 점수를 매기며, `PROC OPTNET`으로
최적화하고, `PROC NETVIZ`로 그린다.

## 대표 노트북 — ICIJ 역외 유출 사기 분석

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)는 실제
**ICIJ 파라다이스 페이퍼스** 유출 데이터(163,435개 노드 — 역외
엔터티, 임원, 주소, 중개기관)를 대상으로 엔드투엔드 사기 분석
파이프라인을 실행한다. `LIBNAME … GRAPH ENGINE=NEO4J`로 연결하고,
`PROC GQL`로 탐색하며, `PROC NETWORK`으로 위험 점수를 매긴다 —
완전한 데이터베이스 기반 그래프 워크플로.

> 이 노트북은 Neo4j 그래프에 연결한다(Jenner Workspace 플랫폼이
> ICIJ 데이터셋을 호스팅한다). 자신의 데이터를 대상으로 실행하려면
> `LIBNAME`을 자신의 Neo4j/Memgraph로 향하게 하라.

## 시각화 데모 — 데이터베이스 불필요

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/)는 역외
소유 그래프를 평범한 데이터셋으로부터 대화형 네트워크 다이어그램으로
렌더링한다 — `jenner` CLI만으로 실행한다:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ 네트워크 다이어그램](../../demos/netviz_showcase/images/example_netviz.png)

## 요구 사항

- `PATH`에 있는 `jenner` 바이너리.
- 그래프 제품군(`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`)의 경우:
  접근 가능한 **Neo4j** 또는 **Memgraph** 인스턴스와 `neo4j` 기능으로
  빌드된 `jenner`.
- `PROC NETVIZ` 데모와 SAS 호환 프로시저는 데이터베이스가 필요 없다.

## 구성

```
notebooks/en/   대표 ICIJ 노트북 (영어)
demos/          netviz_showcase — 데이터베이스 없는 네트워크 다이어그램 데모
i18n/<lang>/    언어별 지역화된 README + 노트북
```

## 언어

이 저장소는 15개 언어로 제공된다. 모든 번역은
[메인 README의 언어 표](../../README.md)를 참조하라.

## 라이선스

MIT. ICIJ 데이터는 © ICIJ이며 해당 약관에 따라 사용된다; 노트북을
참조하라.
