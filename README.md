# Accès à un fournisseur habituel de soins primaires au Canada (2015-2022)

> Analyse de l'évolution de l'accès à un médecin de famille, de ses écarts selon les régions et les groupes de population, et de l'effet de la COVID-19 — démarche **CRISP-DM**, backlog géré dans **Jira**, avec restitution dans **Power BI**. Ce projet est réalisé dans le cadre du module Projet Analyse de données (IFM30518-0020-A2026), session 3 du programme Sciences des données appliquées au Collège La Cité.

---

## Table des matières

1. [Contexte et objectif](#contexte-et-objectif)
2. [Questions analytiques et hypothèses](#questions-analytiques-et-hypothèses)
3. [Données](#données)
4. [Méthodologie](#méthodologie)
5. [Organisation du backlog](#organisation-du-backlog)
6. [Planification des sprints](#planification-des-sprints)
7. [Livrables](#livrables)
8. [Limites connues](#limites-connues)
9. [Structure du dépôt](#structure-du-dépôt)
11. [Auteurs et licence](#auteurs-et-licence)

---

## Contexte et objectif

Ce projet vise à permettre aux **décideurs en santé publique** de comprendre :

- comment l'accès à un fournisseur habituel de soins primaires (indicateur approché du médecin de famille) a **évolué dans le temps** et **selon les régions** ;
- **pourquoi** cet accès diffère (âge, sexe, région, facteurs contextuels) ;
- ce que la **COVID-19** a changé pendant et après la pandémie.

**Parties prenantes visées :** décideurs en santé publique, planificateurs régionaux de santé, analystes de politiques de santé.

## Questions analytiques et hypothèses

Le projet est structuré autour de six questions (Q1 à Q6) reliées chacune à une hypothèse (H1 à H6) :

| # | Thème | Hypothèse / méthode associée |
|---|-------|------------------------------|
| Q1 / H1 | Évolution nationale | Tendance 2015-2019 (régression linéaire simple ou moyenne mobile, IC de la pente) |
| Q2 / H2 | Écarts entre régions | Écart de chaque province à la moyenne nationale, test du seuil de 5 points |
| Q3 / H3 | Groupes de population | Différences de proportions selon l'âge et le sexe |
| Q4 / H4 | Facteurs et composition | Effet de composition vs effet régional (standardisation directe), facteurs contextuels |
| Q5 / H5 | Effet de la COVID-19 | Projection de la tendance d'avant COVID vs valeurs observées |
| Q6 / H6 | Après-COVID | Récupération en 2022 par rapport à 2019 et à la tendance |

## Données

- **Source :** Statistique Canada, tableau **13-10-0096-16** (Enquête sur la santé dans les collectivités canadiennes, ESCC).
- **Indicateur retenu :** « Has a regular healthcare provider » (1 des 32 indicateurs du fichier), part de la population de 12 ans et plus ayant un fournisseur habituel de soins (médecin de famille, spécialiste ou infirmière praticienne).
- **Période :** 2015-2022 (8 années).
- **Géographie :** 10 provinces (territoires absents du jeu de données) + Canada hors territoires comme référence.
- **Ventilations :** groupes d'âge × sexe × géographie.
- **Codes de qualité :** valeurs conservées avec drapeau, **sans imputation** ; les codes `F`, `x` et `..` sont exclus des tests, `E` est signalé.

### Indicateurs dérivés

Taux d'accès, taux de non-couverture (100 − taux d'accès), écart régional, variation en points, effet COVID.

### Périodes d'analyse

| Variable | Modalités |
|----------|-----------|
| Période d'enquête | avant 2022 / 2022 (refonte de l'ESCC) |
| Période COVID | 2015-2019 / 2020-2021 / 2022 |

## Méthodologie

Le projet suit le cycle **CRISP-DM**. Chaque tâche du backlog porte un label indiquant la phase concernée :

`crisp-business-understanding` → `crisp-data-understanding` → `crisp-data-preparation` → `crisp-modeling` → `crisp-evaluation` → `crisp-deployment`

Les retours en arrière entre phases sont identifiés par le label `retour-crispdm`. Les tâches de recherche à durée limitée sont de type **Spike**.

## Organisation du backlog

Le backlog (`Backlog_jira.csv`) contient **96 tickets** : 5 epics, 15 user stories, 76 sous-tâches, pour **76 story points**.

| Epic | Contenu | User stories |
|------|---------|--------------|
| **Définir l'objectif métier** | Cadrage, définition de « accès », périmètre | US-01, US-02 |
| **Portrait de l'accès dans le temps et par région** | Table analytique, tendance nationale, comparaison des provinces, trajectoires régionales | US-03 à US-06 |
| **Comprendre les différences et leurs facteurs** | Âge × sexe, âge × province, standardisation, facteurs contextuels | US-07 à US-10 |
| **Mesurer l'impact de la COVID-19 et l'après-COVID** | Effet COVID, récupération, hétérogénéité | US-11 à US-13 |
| **Communiquer les résultats et recommander** | Tableau de bord Power BI, conclusions et recommandations | US-14, US-15 |

### Conventions

- Un ticket `Story` est rédigé sous la forme « *En tant que… je veux… afin de…* » et précise **ce que j'obtiens**.
- Chaque story se termine par une sous-tâche **Livrable** (label `livrable`).
- Labels : `us-XX` (user story), phase CRISP-DM, thème (`trend`, `covid`, `dashboard`…).

## Planification des sprints

| Sprint | User stories | Story points | Objectif |
|--------|--------------|:------------:|----------|
| **Sprint 1** | US-01, US-02, US-03, US-04 | 16 | Cadrage, table analytique propre, tendance nationale |
| **Sprint 2** | US-05, US-06, US-07 | 15 | Comparaison régionale, trajectoires, groupes âge × sexe |
| **Sprint 3** | US-08, US-09, US-10 | 16 | Zones critiques, standardisation, facteurs contextuels |
| **Sprint 4** | US-11, US-12, US-13 | 16 | Impact et récupération post-COVID, hétérogénéité |
| **Sprint 5** | US-14, US-15 | 13 | Tableau de bord Power BI, conclusions et recommandations |

## Livrables

| Livrable | Story |
|----------|-------|
| Note de cadrage métier | US-01 |
| Glossaire des indicateurs et note de périmètre | US-02 |
| Rapport d'audit de qualité et table analytique nettoyée | US-03 |
| Graphique de tendance nationale annoté | US-04 |
| Classement provincial | US-05 |
| Graphique en petits multiples des trajectoires régionales | US-06 |
| Matrice âge × sexe et fiche des profils les moins couverts | US-07 |
| Carte thermique âge × province | US-08 |
| Graphique taux bruts vs taux standardisés | US-09 |
| Classement des facteurs et note d'interprétation | US-10 |
| Graphique avant/pendant COVID et note méthodologique | US-11 |
| Tableau de récupération par région (vert / orange / rouge) | US-12 |
| Graphique des régions et groupes les plus touchés | US-13 |
| Rapport Power BI interactif publié | US-14 |
| Présentation finale et résumé exécutif | US-15 |

## Limites connues

- Indicateur **approché** : « fournisseur habituel » inclut médecin de famille, spécialiste ou infirmière praticienne.
- Données **auto-déclarées** (enquête).
- **Rupture de série en 2022** (refonte de l'ESCC) et changements de libellé de la question : la comparabilité 2015-2022 est limitée, et l'effet de la refonte peut ne pas se séparer de celui de la COVID-19.
- Collecte pendant la pandémie (2020-2021) pouvant affecter la comparabilité.
- **2022 est la seule année après la pandémie** dans les données.
- Faibles effectifs et estimations supprimées pour les petites provinces et certains croisements.
- Analyses **associatives uniquement** : aucune conclusion causale.
- Hors périmètre : délais d'attente, qualité des soins, besoins non comblés, causalité.

## Structure du dépôt

```

├── README.md
├── Backlog_jira.csv        # Backlog complet (epics, stories, sous-tâches)
├── data/
├── notebooks/
├── powerbi/           
├── figures/                     
└── livrables/

```

## Auteurs et licence

- **Équipe de développement :** Fatima Zohra Aboudeine · Safaa Namane · Badr Kabbadj · Mohamed Ali Alaoui
- **Encadrement / Scrum Master :** Dr Nacereddine Benzebouchi
- **Licence :** ## Contient de l'information visée par la [Licence du gouvernement ouvert – Canada](https://ouvert.canada.ca/fr/licence-du-gouvernement-ouvert-canada).
