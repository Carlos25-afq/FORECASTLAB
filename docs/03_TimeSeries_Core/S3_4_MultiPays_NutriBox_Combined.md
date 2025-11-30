# Cas 3.4 — Prévision combinée multi-pays NutriBox  
NOVAFOOD GLOBAL — Méthodes top-down, bottom-up, middle-out & forecast blending

---

## 1. Résumé du cas

NutriBox est vendue dans quatre marchés stratégiques :

- 🇫🇷 France  
- 🇲🇦 Maroc  
- 🇧🇷 Brésil  
- 🇻🇳 Vietnam  

Chaque pays possède :

- un profil de demande différent,  
- un niveau de maturité marché variable,  
- une saisonnalité propre,  
- une volatilité distincte.

NOVAFOOD GLOBAL doit construire une **prévision consolidée “Global NutriBox”**, puis redistribuer cette prévision dans chaque pays.

Ce cas te place dans la peau du **Global Demand Planner NutriBox**, chargé de :

- combiner des prévisions locales,  
- définir une prévision globale robuste,  
- redistribuer les volumes via des méthodes hiérarchiques.  

---

## 2. Compétences visées

- Comprendre les approches **bottom-up**, **top-down**, **middle-out**  
- Réaliser une **fusion de prévisions** (forecast blending)  
- Utiliser des **pondérations statistiques** : inverse MAPE, variance inverse  
- Construire une prévision globale cohérente et soutenable  
- Redistribuer la prévision globale au niveau pays  
- Rédiger une communication claire pour le S&OP Global  

---

## 3. Contexte NOVAFOOD — NutriBox Global

Les quatre pays présentent :

| Pays | Saison | Volatilité | Maturité | Contrainte |  
|------|---------|--------------|-----------|-------------|  
| France | Forte | Moyenne | Haute | Promotions régulières |  
| Maroc | Moyenne | Haute | Moyenne | Ramadan impact |  
| Brésil | Faible | Très forte | Moyenne | Hausses prix |  
| Vietnam | Moyenne | Forte | Haute | Effet météo fort |

L’enjeu est **critique**, car :

- NutriBox représente **28% du CA global** de NOVAFOOD  
- La production France doit anticiper 6 mois d’avance  
- Les hubs logistiques doivent préparer les stocks APAC, EMEA & LATAM  

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S3_4_NutriBox_MultiPays.csv`

 

---

## 5. Travail demandé — Étapes détaillées

### Étape 1 — Analyse prévision locale

Pour chaque pays :

1. Tracer `Demand` vs `Forecast_Local`  
2. Calculer :
   - MAPE  
   - RMSE  
   - Biais  
   - Variance  

📌 **Question 1 :**  
Quel pays a la prévision locale la plus fiable ? Le moins fiable ?

---

### Étape 2 — Prévision globale (méthode bottom-up)

1. Additionner les tendances locales  
2. Obtenir un **forecast Global NutriBox**  
3. Comparer au global réel (si fourni)

📌 **Question 2 :**  
La somme des prévisions locales offre-t-elle une prévision solide ?

---

### Étape 3 — Prévision globale (méthode top-down)

1. Construire une prévision globale via :
   - Holt-Winters global  
   - ou ARIMA global  
2. Redistribuer par poids historiques :
   - Poids en volume  
   - Poids en CA  
   - Poids en part de marché

📌 **Question 3 :**  
Quel critère de redistribution est le plus stable pour NutriBox ?

---

### Étape 4 — Forecast fusion (blending)

Méthode recommandée : **pondération inverse MAPE**

\[
Forecast_{combined} = \frac{\sum (Forecast_i / MAPE_i)}{\sum (1 / MAPE_i)}
\]

Ou version robustifiée : inverse variance.

3 modèles :

- Bottom-up  
- Top-down  
- Weighted-blend  

Comparer :

- AIC global  
- MAPE global  
- Robustesse  

📌 **Question 4 :**  
Quel modèle recommandez-vous globalement ? Pourquoi ?

---

### Étape 5 — Méthode middle-out (niveau Europe)

Créer :

- forecast par cluster  
- puis diffusion dans les pays

Exemple cluster :  

- **EMEA = FR + MA**  
- **LATAM = BR**  
- **APAC = VN**

📌 **Question 5 :**  
Quels clusters permettent la prévision la plus fiable ?

---

### Étape 6 — Narration S&OP Global

Synthétiser :

- message clé global NutriBox  
- risques multi-régions  
- arbitrages (production France, capacités logistiques)  

📌 **Question 6 :**  
Rédigez une note S&OP globale (8–10 lignes) pour le COMEX.

---

## 6. Livrables attendus

- Excel ou notebook :  
  - prévisions locales  
  - fusion  
  - top-down / bottom-up / middle-out  
- Graphiques multi-pays  
- Tableau comparatif  
- Note S&OP Global NutriBox  

---

## 7. Critères d’évaluation

- Compréhension hiérarchique des séries  
- Capacité à combiner plusieurs prévisions  
- Justification statistique du modèle choisi  
- Cohérence avec contraintes business  
- Clarté de la rédaction S&OP  

---

## 8. Extensions (niveau expert)

- Hierarchical Forecasting (Hyndman)  
- Reconciliation (MinT, OLS, WLS)  
- Multi-level ARIMA  
- Forecast probabiliste global  
- Elasticité cross-countries  

---
