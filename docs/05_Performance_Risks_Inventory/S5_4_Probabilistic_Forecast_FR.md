# Cas 5.4 — Prévision Probabiliste FreshBite France  
Forecast Min / Base / Max — Quantiles, risque & arbitrages S&OP  
NOVAFOOD GLOBAL – Gamme FreshBite

---

## 1. Résumé du cas

La gamme **FreshBite France** (plats frais végétariens premium) connaît une forte volatilité, liée à :

- une saisonnalité marquée (été/printemps),
- des promotions très agressives en GMS (10–40%),
- une concurrence croissante,
- des périodes d’innovations produits fréquentes.

La Direction France souhaite abandonner la prévision “single number” jugée trop rigide, trop optimiste ou trop pessimiste selon les cycles.

Elle veut désormais un **forecast probabiliste**, comprenant :

- **P10 — Forecast pessimiste (min)**
- **P50 — Forecast médian (base)**
- **P90 — Forecast optimiste (max)**

Vous êtes le **Demand Planner FreshBite France**, chargé de :

1. Construire un **range forecast** basé sur les distributions d’erreurs,  
2. Estimer les quantiles P10/P50/P90,  
3. Mesurer le risque de rupture associé,  
4. Proposer la valeur de consensus à utiliser en S&OP,  
5. Donner les implications pour les stocks, le service et la production.

---

## 2. Compétences visées

- Compréhension du forecast probabiliste  
- Analyse de quantiles  
- Modélisation de l’incertitude  
- Construction d’un range forecast  
- Utilisation du forecast Min/Base/Max dans le S&OP  
- Traduction du risque en niveau de service et en stock de sécurité  
- Communication d’un forecast incertain  
- Présentation d’une recommandation stratégique  

---

## 3. Dataset

📂 Dataset recommandé :  
`datasets/novfood_case_studies/S5_4_Probabilistic_FreshBite_FR.csv`


---

## 4. Travail demandé — Étapes détaillées

---

### 🔹 Étape 1 — Analyse de la distribution d’erreurs

1. Tracer l’histogramme des erreurs  
2. Calculer :
   - moyenne,
   - médiane,
   - skewness,
   - kurtosis,
   - min/max.  
3. Déterminer si la distribution :
   - est normale,  
   - skewed,  
   - heavy-tailed (kurtosis > 3),  
   - comporte des outliers.

📌 **Question 1 : Comment qualifier la distribution des erreurs FreshBite France ?**

---

### 🔹 Étape 2 — Calcul des quantiles (P10 / P50 / P90)

À partir des erreurs historiques :

- P10 = scénario pessimiste  
- P50 = scénario médian (forecast classique)  
- P90 = scénario optimiste  

\[
Forecast_{P10} = Forecast\_Base + Error\_{P10}
\]

\[
Forecast_{P50} = Forecast\_Base + Error\_{P50}
\]

\[
Forecast_{P90} = Forecast\_Base + Error\_{P90}
\]

📌 **Question 2 : Quel est le range forecast (min/base/max) pour FreshBite France ?**

---

### 🔹 Étape 3 — Simulation probabiliste (optional but premium)

Simuler 20 000 demandes futures :

- échantillonnage d’erreurs selon la distribution réelle,  
- ajout au forecast base,  
- obtention d’un histogramme des forecasts possibles.

Sorties attendues :

- distribution complète des prévisions,  
- probabilité de dépasser le forecast base,  
- probabilité de rupture selon seuil de stock,  
- fan chart (graphique en éventail).

📌 **Question 3 : Quelle est la probabilité que la demande dépasse P90 ?**

---

### 🔹 Étape 4 — Lien avec le stock de sécurité

Le range forecast influence directement le SS :

- SS(P50) = stock classique  
- SS(P90) = stock “haute protection”  
- SS(P10) = risque maximal de rupture

À l’aide du stock actuel :

- évaluer si le stock couvre P50,  
- calculer la probabilité de rupture,  
- estimer les coûts liés aux ruptures.

📌 **Question 4 : Le stock actuel protège-t-il P50 ? P90 ?**

---

### 🔹 Étape 5 — Arbitrage S&OP

Proposer un arbitrage clair entre :

- service client,
- risque de rupture,
- risque de surstock,
- impact cash,
- capacité production.

Dans un vrai S&OP :  
→ **P50 est la valeur de consensus**,  
→ mais P10/P90 sont essentiels pour :

- dimensionner la supply,  
- évaluer les risques,  
- planifier financièrement.

📌 **Question 5 : Quelle valeur recommandez-vous en consensus forecast pour FreshBite FR ? Pourquoi ?**

---

### 🔹 Étape 6 — Recommandation business

Rédiger une note synthétique (10–12 lignes) pour :

- expliquer le range forecast,
- préciser le risque de rupture selon P50/P90,
- proposer un niveau de service cible,
- recommander un SS adapté,
- indiquer l’impact cash,
- préciser les actions court terme (promo, distribution, production).

📌 **Question 6 : Rédigez une recommandation complète au Directeur France.**

---

## 5. Livrables attendus

- Range forecast (P10/P50/P90)
- Graphique du fan chart (optional but premium)
- Tableau risques / coûts / service
- Recommandation S&OP écrite
- Simulation Monte Carlo (si Python)

---

## 6. Critères d’évaluation

- Qualité des quantiles  
- Bonne compréhension du forecast probabiliste  
- Pertinence du consensus  
- Clarté des risques  
- Cohérence business  
- Communication S&OP crédible  

---

## 7. Extensions (niveau expert)

- Fan chart animé (Python / Plotly)  
- Range forecast par canal (Retail vs Drive vs E-commerce)  
- Forecast probabiliste multi-capacité (production + transport)  
- Modèle mixte : ML + probabilistic range  
- Couplage au Safety Stock dynamique  

---
