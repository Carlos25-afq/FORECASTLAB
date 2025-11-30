# 02 — Data Tools for Demand Planners  
NOVAFOOD GLOBAL — Data Engineering, Analytics & Automation

La performance du Demand Planner repose sur trois piliers :  
1. **La qualité des données**  
2. **La capacité à les transformer rapidement**  
3. **La capacité à automatiser le flux analytique**

Cette section fournit toutes les briques techniques utilisées par NOVAFOOD GLOBAL pour construire un système robuste de prévisions et de pilotage basé sur les données.  
Elle couvre Excel avancé, Power Query, Power Pivot / DAX, VBA, SQL et l’ingénierie de données minimale attendue d’un Demand Planner moderne.

---

# 🎯 Objectifs de la section

À l’issue de cette section, vous serez capable de :

- Nettoyer et structurer des datasets volumineux (jusqu’à plusieurs millions de lignes)  
- Construire un **Fact_Demand** complet pour 18 pays  
- Déployer un modèle en étoile (Power Pivot / Power BI)  
- Implémenter des mesures DAX professionnelles (MAPE, biais, rolling forecasts)  
- Automatiser des workflows via Power Query et VBA  
- Utiliser SQL pour manipuler l’historique ventes multi-pays  
- Intégrer les flux dans un pipeline cohérent pour NOVAFOOD

---

# 🧩 1. Excel — Fondations avancées

Excel reste l’outil le plus utilisé chez NOVAFOOD pour les analyses rapides et les simulations locales.

### 1.1 Fonctions avancées essentielles
- **XLOOKUP** / INDEX + MATCH  
- **SUMIFS / COUNTIFS** multi-critères  
- **IFS / SWITCH**  
- **TEXT / LEFT / RIGHT / MID**  
- **DATE, EDATE, WORKDAY, EOMONTH**  
- Fonctions matricielles (SEQUENCE, FILTER, UNIQUE…)

### 1.2 Tableaux et modélisation
- Tableaux structurés (Table1…)  
- Mesures dans Power Pivot  
- Segments & filtres dynamiques  
- Visualisations “Clean Dashboard”

### 1.3 Cas d’usage NOVAFOOD
- Préparation manuelle d’un **baseline forecast**  
- Analyse MoM / YoY par marque  
- Construction de scénarios prix/promo

---

# 🧩 2. Power Query — Premier pipeline de données NOVAFOOD

Power Query est le moteur d’ingestion principal de NOVAFOOD pour les données CSV, ERP Export, POS, e-commerce et MDM.

### 2.1 Sources multi-pays
- France → ventes quotidiennes  
- Maroc → ventes hebdomadaires agrégées  
- Brésil → e-commerce (SKU-level)  
- Vietnam → production + consommations matières  
- POS Retail (Belgique, Kenya, Malaisie)

### 2.2 Transformations
- Nettoyage (trim, null replace, type corrections)  
- Unpivot / pivot  
- Merge (join) sur clé produit / canal / pays  
- Création du calendrier complet (dim_date)  
- Harmonisation UOM (unités)

### 2.3 Flux Power Query type NOVAFOOD
- `RAW_INPUT/` → `QUERY/` → `MODEL/`  
- Actualisation automatique via VBA ou Power BI Service  

---

# 🧩 3. Power Pivot / DAX — Modèle en étoile et KPIs de prévision

NOVAFOOD utilise un modèle en étoile standardisé pour toutes les zones.

### 3.1 Tables principales
- **Fact_Demand**  
- **Dim_Product**  
- **Dim_Customer**  
- **Dim_Channel**  
- **Dim_Time**  
- **Dim_Country**

### 3.2 Mesures DAX essentielles
- **Total Sales**  
- **Forecast Error (Actual - Forecast)**  
- **MAPE** (version robuste)  
- **BIAS**  
- **Service Level**  
- **Rolling 3/6/12 months**  
- **YoY Growth**  
- **Promo Lift %**

### 3.3 Time Intelligence (indispensable)
- SAMEPERIODLASTYEAR  
- DATEADD  
- YTD / MTD / QTD  

---

# 🧩 4. VBA — Automatisation & Productivité

VBA est utilisé chez NOVAFOOD pour :

- automatiser les refresh Power Query  
- générer les rapports PDF (Weekly Forecast Report)  
- créer des fichiers exports propres à envoyer aux usines  
- envoyer des alertes (prévisions vs capacité)

### Automatisations typiques
- Rafraîchissement dataset complet
- Export automatique du Consensus Forecast
- Génération fichiers “Allocation” par pays

---

# 🧩 5. SQL & Data Engineering Minimal

Bien qu’un Demand Planner ne soit pas Data Engineer, chez NOVAFOOD il doit savoir :

### 5.1 Extraire & filtrer
```sql
SELECT *
FROM Fact_Demand
WHERE Country = 'Morocco'
AND Year = 2024;

5.2 Construire des vues analytiques
CREATE VIEW v_ForecastAccuracy AS
SELECT Country, SKU,
       AVG(ABS((Actual - Forecast)/Actual)) AS MAPE
FROM Fact_Demand
GROUP BY Country, SKU;

5.3 Joindre plusieurs sources
SELECT f.*, p.Category, c.ChannelName
FROM Fact_Demand f
LEFT JOIN Dim_Product p ON f.SKU = p.SKU
LEFT JOIN Dim_Channel c ON f.ChannelID = c.ID;

🧪 CAS PRATIQUES NOVAFOOD
2.1 : Nettoyer 1,2M lignes de ventes NOVAFOOD

Objectif :
Nettoyer un dataset multi-pays contenant erreurs, doublons, valeurs manquantes et bruit.

Livrables :

Script Power Query

Rapport qualité de données

Fichier clean .xlsx

2.2 : Dashboard Power BI Forecast vs Actuals (Europe)

Objectif :
Construire un dashboard complet en utilisant DAX & Power Query.

Livrables :

.pbix

Pages : Overview, Monthly Accuracy, Rolling 12m, Drilldown SKU

2.3 : SQL — reconstruire historique Maroc

Objectif :
Fusionner 3 sources marocaines incohérentes dans un Fact_Demand cohérent.

Livrables :

Script SQL

Fichier transformé

Vérification 10 KPI qualité

2.4 : Automatisation VBA — export forecast quotidien

Objectif :
Générer automatiquement un fichier forecast journalier pour les usines.

Livrables :

Script .bas

Exemple exporté

Documentation utilisateur

📌 Navigation

Section 3 — Core Time Series Forecasting
