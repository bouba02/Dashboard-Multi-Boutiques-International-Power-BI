# Dashboard Retail International — 306 Boutiques · 16 Pays | Power BI

> **500M€ CA · 148 000 transactions · 1 689 produits · 3 continents**  
> 3 dashboards · 30+ mesures DAX · Star Schema 6 tables · Time Intelligence

🇬🇧 [English version available here](README.md)

---

## Contexte du Projet

Analyse de la performance d'un réseau retail international de 306 boutiques
opérant sur 16 pays et 3 continents — couvrant les ventes, le catalogue produits
et la performance des points de vente sur 2 ans (2020–2021).

**Périmètre :**

| Dimension | Valeur |
|---|---|
| CA Total | **500,40M€** |
| Transactions | **148 000+** |
| Produits | **1 689** |
| Boutiques | **306** (Store · Online · Reseller · Catalog) |
| Pays | **16** — 3 continents |
| Employés | **11 000** |

---

## Dashboards — 3 Pages

### Dashboard 1 — Ventes
![Ventes](dashboard_page_3.png)
CA · Unités vendues · Croissance YoY · Analyse par catégorie, marque et classe · Évolution temporelle

### Dashboard 2 — Produits
![Produits](dashboard_page_2.png)
Catalogue 1 689 références · Analyse retours vs ventes · Top 3 produits · Distribution par catégorie et sous-catégorie · Taux de retour par segment

### Dashboard 3 — Boutiques
![Boutiques](dashboard_page_1.png)
306 boutiques · Répartition géographique (16 pays · 3 continents) · Performance par type de canal · 11 000 employés

---

## Modèle de Données — Star Schema

```
              [Dim_Date]
                  │
      ┌───────────┼───────────┐
      │           │           │
[Dim_Produit] [Fact_Sales] [Dim_Boutique]
  1 689 réf.   148 000+    306 boutiques
      │         lignes          │
      ▼                         ▼
[Dim_Categorie]          [Dim_Geographie]
  5 catégories              16 pays
```

**6 tables · Relations Many-to-One · Filtres cross-page synchronisés**

---

## Mesures DAX — 30+ Mesures

```dax
// Chiffre d'affaires
CA = SUM(Sales[Montant de Vente])

// Comparaison année précédente
CA_N1 = CALCULATE([CA], DATEADD(Dim_Date[Date], -1, YEAR))

// Croissance YoY
Ecart_CA_% = DIVIDE([CA] - [CA_N1], [CA_N1], 0)

// Volume
Nbre_Ventes    = COUNTROWS(Sales)
Quantite_Vendue = SUM(Sales[Quantité de vente])

// Rentabilité
Avg_Profit_Margin = DIVIDE([Profit Total], [CA], 0)

// Qualité
Taux_Retour = DIVIDE(
    SUM(Sales[Quantité de retour]),
    SUM(Sales[Quantité de vente]),
    0
)
```

**Patterns avancés utilisés :** Time Intelligence · CALCULATE · DATEADD · DIVIDE · Conditional formatting dynamique

---

## Fonctionnalités du Dashboard

- Navigation multi-pages avec boutons interactifs
- Slicers synchronisés cross-page (Année · Mois · Pays · Boutique)
- 8 types de visualisations (gauges · donut · line charts · tables · barres)
- Palette design cohérente — orange `#EB601B` / bleu marine

---

## Stack Technique

- **Power BI Desktop** — 3 dashboards, navigation multi-pages
- **Power Query / M** — consolidation de 6 fichiers CSV trimestriels (2020–2021)
- **DAX** — 30+ mesures avec Time Intelligence
- **Star Schema** — 6 tables, modélisation multi-dimensionnelle

---

## Installation

```bash
git clone https://github.com/bouba02/Dashboard-Multi-Boutiques-International.git
```

Ouvrir `Dashboard Boutique.pbix` dans Power BI Desktop.  
`Accueil → Actualiser` — les fichiers CSV sont automatiquement chargés.

---

## Structure du Repository

```
Dashboard-Multi-Boutiques-International/
├── README.md
├── README_FR.md
├── Dashboard Boutique.pbix
├── Dashboard Boutique.pdf
├── Dashboards/
│   ├── dashboard_page_1.png    # Boutiques
│   ├── dashboard_page_2.png    # Produits
│   └── dashboard_page_3.png    # Ventes
└── dataset/
    ├── Geographie.csv
    ├── Boutiques.csv
    ├── Produits.csv
    ├── Categorie Produits.csv
    ├── Sous Categories Produits.csv
    └── Sales/
        ├── Sales 2020 T1.csv … Sales 2021 T3.csv
```

---

## Auteur

**Boubacar Nikiema** — Data Analyst & Consultant BI

Spécialisé en dashboards retail & distribution, analytics multi-entités et pilotage
de la performance avec Power BI, SQL, Python et Excel. Basé au Maroc, j'interviens
auprès d'entreprises en Afrique et en Europe francophone.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-boubacar--nikiema-blue?logo=linkedin)](https://linkedin.com/in/boubacar-nikiema)
[![YouTube](https://img.shields.io/badge/YouTube-BoubacarDataAnalyst-red?logo=youtube)](https://youtube.com/@BoubacarDataAnalyst)
[![Email](https://img.shields.io/badge/Email-nikiemaboubacar%40gmail.com-gray?logo=gmail)](mailto:nikiemaboubacar@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-data.ngroupmediadigital.com-green)](https://data.ngroupmediadigital.com)

---

*Données simulées · Code : MIT License*
