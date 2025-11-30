# Cas 5.1 — MAPE & Forecast Value Added pour 10 000 SKU multi-pays  
NOVAFOOD GLOBAL — Pilotage de la performance du processus de prévision

---

## 1. Résumé du cas

NOVAFOOD GLOBAL dispose d’un portefeuille de plus de **10 000 SKU** vendus dans 18 pays, via plusieurs canaux (Retail, E-commerce, Food Service).

Chaque mois, le processus de prévision génère :

- une **prévision statistique de base** (Stat_Forecast),
- des **ajustements Sales**, Marketing, Finance,
- un **Consensus Forecast** final.

La Direction Supply Chain demande :

1. Une **mesure claire de la qualité de prévision (MAPE, Biais, etc.)** à différents niveaux.  
2. Une **analyse Forecast Value Added (FVA)** pour savoir **qui améliore** la prévision… et qui la détériore.  
3. Une classification des SKU selon leur **forecastability** pour adapter les efforts.

Vous êtes le **Demand Planner Performance Lead** chargé de :

- analyser 10 000 SKU multi-pays,  
- calculer les métriques d’erreur,  
- évaluer la FVA par étape du processus,  
- fournir une recommandation structurée pour améliorer le processus.

---

## 2. Compétences visées

### 📏 Mesure de la performance
- Calcul MAPE, MAE, RMSE, Biais  
- Comparaison de modèles / versions de prévision  
- Agrégation d’erreurs par pays / gamme / canal  

### 📈 Forecast Value Added (FVA)
- Construction d’un **naïf de référence**  
- Évaluation FVA par étape :
  - Stat_Forecast
  - Sales_Adjust
  - Marketing_Adjust
  - Finance_Adjust
  - Consensus_Forecast  
- Identification des étapes **VA** (Value Added), **NNVA** (Necessary Non Value Added) et **NVA** (Non Value Added)

### 🧠 Analyse de portefeuille
- Segmentation selon MAPE & biais  
- Identification des SKU à forte variabilité  
- Préconisation de stratégies différenciées

---

## 3. Contexte NOVAFOOD — Portefeuille 10 000 SKU

Périmètre :

- Pays : France, Maroc, Brésil, Vietnam, Belgique, Kenya, Malaisie, etc.  
- Horizon analysé : 12 mois  
- Granularité : mensuelle  
- Niveaux :
  - SKU  
  - Pays  
  - Gamme (NutriBox, EcoPure, FreshBite, VitalMeal, etc.)

Le processus de prévision comprend :

1. **Naïf de base** : `Naive_Fcst` (ex : last year same month)  
2. **Prévision statistique** : `Stat_Fcst` (lissages, Holt-Winters, ARIMA…)  
3. **Ajustements Sales** : `Sales_Fcst`  
4. **Ajustements Marketing** : `Mkt_Fcst`  
5. **Ajustements Finance / Management** : `Mgmt_Fcst`  
6. **Consensus final** : `Final_Fcst`

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S5_1_FVA_10000SKU_MultiCountry.csv`



---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Calcul des métriques d’erreur par version de forecast

Pour chaque combinaison (`SKU`, `Country`, `Date`) :

Calculer :

- MAPE (par version de forecast)
- MAE
- Biais (ME ou MPE)
- RMSE (optionnel)

Pour :

- `Naive_Fcst`  
- `Stat_Fcst`  
- `Sales_Fcst`  
- `Mkt_Fcst`  
- `Mgmt_Fcst`  
- `Final_Fcst`

📌 **Question 1 :**  
En moyenne, **quelle version de forecast est la plus précise** (MAPE le plus bas) ?  
La prévision naïve est-elle vraiment moins bonne que les autres ?

---

### Étape 2 — Calcul du Forecast Value Added (FVA)

Pour chaque étape, calculer :

\[
FVA\_{Étape} = MAPE\_{Référence} - MAPE\_{Étape}
\]

Où :

- Référence = `Naive_Fcst` (ou `Stat_Fcst`, selon la définition choisie)  
- Étapes successives : Stat, Sales, Mkt, Mgmt, Final.

Interprétation :

- FVA > 0 : étape améliore la prévision (VA)  
- FVA ≈ 0 : étape neutre (NNVA)  
- FVA < 0 : étape détériore la prévision (NVA)

📌 **Question 2 :**  
Quelles étapes du processus **créent réellement de la valeur** sur le portefeuille global ?

---

### Étape 3 — Analyse FVA par région / gamme

Segmenter les résultats :

- Par pays  
- Par marque (NutriBox, EcoPure, FreshBite, VitalMeal)  
- Par canal (Retail, E-commerce, Food Service)

Identifier les patterns :

- Les Sales améliorent-ils la prévision partout ?  
- Marketing **détruit-il** parfois la performance ?  
- Certains pays sont-ils **sur-ajustés** ?

📌 **Question 3 :**  
Dans quels pays ou gammes les interventions humaines détériorent-elles le plus le forecast ?

---

### Étape 4 — Segmentation Forecastability du portefeuille

Construire une classification des SKU selon :

- MAPE `Final_Fcst`  
- Biais  
- Volatilité (CV = σ / μ)  
- Volume moyen

Exemples de classes :

- **Classe A** : MAPE < 15%, volume élevé  
- **Classe B** : 15–30%, volume moyen  
- **Classe C** : 30–50%, instable  
- **Classe D** : > 50%, “unforecastable”

📌 **Question 4 :**  
Quelle proportion de SKU est dans les classes C et D ?  
Qu’implique cela en termes de stratégie de prévision ?

---

### Étape 5 — Analyse multi-niveaux (agrégation)

Comparer les MAPE :

- par SKU  
- par gamme  
- par pays  
- global

Observer :

- l’effet de l’agrégation sur la précision  
- la cohérence entre niveaux (SKU vs gamme vs global)

📌 **Question 5 :**  
À quel niveau l’erreur de prévision est-elle la plus faible ? Pourquoi ?

---

### Étape 6 — Recommandations de refonte du processus

Sur la base des résultats FVA + Forecastability :

- identifier les étapes à **alléger** ou **automatizer**,  
- proposer des règles de **gouvernance** :
  - quels SKU doivent être principalement gérés par stats ?  
  - où les Sales/Marketing ajoutent-ils de la vraie valeur ?  
- définir les **KPI à suivre régulièrement**.

📌 **Question 6 :**  
Rédigez une note à la Direction Supply Chain expliquant comment **re-designer le processus** pour maximiser le FVA.

---

## 6. Livrables attendus

- Fichier Excel ou notebook Python avec :
  - calcul des erreurs pour chaque version de forecast,  
  - calcul du FVA par étape et par segment,  
  - matrice de forecastability.

- Visualisations recommandées :
  - barplot FVA par étape,  
  - heatmap FVA par pays / gamme,  
  - histogramme MAPE distribution des SKU.

- Note synthétique (1 page max) pour la Direction Supply Chain.

---

## 7. Critères d’évaluation

- Correctitude des métriques d’erreur  
- Bonne définition du FVA  
- Analyse pertinente par segment (pays, gamme, canal)  
- Qualité de la segmentation Forecastability  
- Recommandations process claires, actionnables, réalistes  

---

## 8. Extensions (niveau expert)

- FVA dynamique dans le temps (rolling)  
- Lien entre FVA et niveau de stock / service  
- Corrélation entre forecastability et type de modèle utilisé  
- Introduction d’un **Forecastability Index** global  
- Dashboards FVA dans Power BI (section Data Tools)

---
