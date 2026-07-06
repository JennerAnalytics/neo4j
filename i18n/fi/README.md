# Neo4j ja verkkoanalyysi Jennerillä

[Jenner](https://jenneranalytics.com) tuo graafitietokannat ja
verkkoanalyysin SAS-yhteensopivaan DATA step- ja PROC-maailmaan. Yhdistä
**Neo4j**- tai **Memgraph**-tietokantaan `LIBNAME`-lauseella, tee niihin
kyselyitä **Cypher/GQL**-kielellä, aja graafi**algoritmeja**, piirrä
**interaktiivisia verkkokaavioita** ja käytä silti **SAS-yhteensopivia**
verkon optimointi- ja analyysiproseduureja — kaikki yhdessä ohjelmassa.

Tämä tietovarasto esittelee koko pinon, ankkuroituna todelliseen
lippulaivamuistikirjaan ja tietokannattomaan visualisointidemoon. Kaikki
on tarjolla **15 kielellä** (katso [Kielet](#kielet)).

## Ominaisuudet

### Uutta — Jennerin graafiperhe (ei SAS-vastinetta)

| Ominaisuus | Mitä se tekee |
|---|---|
| **`LIBNAME … GRAPH ENGINE=NEO4J`** (tai `MEMGRAPH`) | Sido graafitietokanta librefiin, kuten mikä tahansa muu kirjasto. |
| **`PROC GQL`** | Aja **Cypher / GQL** -kyselyitä graafia vastaan ja kirjoita tulosjoukko Jenner-datajoukkoon. |
| **`PROC LINKS`** | Aja graafi**algoritmeja** — PageRank, yhteisöjen tunnistus, lyhin polku, keskeisyys — graafia vastaan ja kirjoita solmu-/reunakohtaiset tulokset datajoukkoon. |
| **`PROC NETVIZ`** | Piirrä graafi **interaktiivisena Cytoscape.js**-verkkokaaviona (upotettuna Jupyter-ytimeen tai itsenäisenä HTML-tiedostona komentoriviltä). |

### SAS-yhteensopivat verkkoproseduurit

| Ominaisuus | Mitä se tekee |
|---|---|
| **`PROC OPTNET`** | Verkon **optimointi** Jenner-datajoukoilla — lyhin polku, TSP, minimikustannusvirtaus, yhtenäiset komponentit, syklit, klikit ja paljon muuta. Sovitus SAS/OR PROC OPTNETistä. |
| **`PROC NETWORK`** | Klassinen verkon **analyysi** Jenner-datajoukoilla — keskeisyydet, yhteisöt, kaksitahoisesti yhtenäiset komponentit, polut. Sovitus SAS Viya PROC NETWORKista. |

Uusi perhe toimii **elävällä graafitietokannalla**; SAS-yhteensopivat
proseduurit toimivat **reuna-/solmudatajoukoilla**, jotka sinulla jo on.
Ne yhdistyvät: nouda aligraafi `PROC GQL`:llä, pisteytä se `PROC
LINKS`:llä tai `PROC NETWORK`:llä, optimoi `PROC OPTNET`:llä ja piirrä se
`PROC NETVIZ`:llä.

## Lippulaivamuistikirja — ICIJ offshore-leaks -petosanalytiikka

[`icij_fraud_analytics.ipynb`](icij_fraud_analytics.ipynb)
suorittaa päästä päähän petosanalytiikan putken todellista **ICIJ
Paradise Papers** -vuotoa vastaan (163 435 solmua — offshore-yhteisöjä,
toimihenkilöitä, osoitteita ja välittäjiä). Se muodostaa yhteyden
`LIBNAME … GRAPH ENGINE=NEO4J`:llä, tutkii `PROC GQL`:llä ja pisteyttää
riskin `PROC NETWORK`:llä — täydellinen, tietokantaan tukeutuva
graafityönkulku.

> Muistikirja muodostaa yhteyden Neo4j-graafiin (Jenner Workspace -alusta
> isännöi ICIJ-datajoukkoa). Osoita `LIBNAME` omaan Neo4j-/Memgraph-
> instanssiisi ajaaksesi sen omaa dataasi vastaan.

## Visualisointidemo — tietokantaa ei tarvita

[`../../demos/netviz_showcase/`](../../demos/netviz_showcase/) piirtää
offshore-omistusgraafin interaktiivisena verkkokaaviona tavallisista
datajoukoista — aja se pelkällä `jenner`-komentorivityökalulla:

```bash
jenner demos/netviz_showcase/demo.jenner .
# -> demos/netviz_showcase/offshore_network.html
```

![PROC NETVIZ -verkkokaavio](../../demos/netviz_showcase/images/example_netviz.png)

## Vaatimukset

- `jenner`-binääri `PATH`-polussasi.
- Graafiperheelle (`LIBNAME GRAPH`, `PROC GQL`, `PROC LINKS`): tavoitettava
  **Neo4j**- tai **Memgraph**-instanssi ja `neo4j`-ominaisuudella käännetty
  `jenner`.
- `PROC NETVIZ` -demo ja SAS-yhteensopivat proseduurit eivät tarvitse
  tietokantaa.

## Rakenne

```
notebooks/en/   lippulaiva-ICIJ-muistikirja (englanti)
demos/          netviz_showcase — tietokannaton verkkokaaviodemo
i18n/<kieli>/   lokalisoitu README + muistikirja kieltä kohden
```

## Kielet

Jokaisessa kielikansiossa on lokalisoitu README ja käännetty muistikirja:

| | | | |
|---|---|---|---|
| [Čeština](../cs/README.md) | [Dansk](../da/README.md) | [Deutsch](../de/README.md) | [Ελληνικά](../el/README.md) |
| [Español](../es/README.md) | [Suomi](../fi/README.md) | [Français](../fr/README.md) | [Italiano](../it/README.md) |
| [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Nederlands](../nl/README.md) | [Polski](../pl/README.md) |
| [Português](../pt/README.md) | [Svenska](../sv/README.md) | [中文](../zh/README.md) | [English](../../README.md) |

## Lisenssi

MIT. ICIJ-data on © ICIJ ja käytetty heidän ehtojensa mukaisesti; katso
muistikirja.
