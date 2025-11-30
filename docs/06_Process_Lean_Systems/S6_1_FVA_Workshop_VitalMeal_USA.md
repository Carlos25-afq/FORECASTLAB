# Cas 6.1 — Atelier Forecast Value Added (FVA) : VitalMeal USA  
Analyse Lean du processus de prévision — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

La gamme **VitalMeal USA** (nutrition sportive premium) souffre d’un **MAPE > 32%**, malgré de nombreuses interventions manuelles dans le processus forecast → consensus.

Les principales étapes du flux prévisionnel USA :

1. **Statistical Forecast** (modèle automatique SAP IBP)  
2. **Sales Override** (ajustements commerciaux)  
3. **Marketing Review**  
4. **Finance Review**  
5. **Consensus Forecast**  
6. **Final S&OP Validation**

Les dirigeants soupçonnent :

- un excès de modifications manuelles,
- des sur-ajustements incohérents,
- des overrides qui **dégradent** l’accuracy,
- de la politique commerciale influençant les chiffres.

Vous êtes mandaté comme **Demand Planner Senior** pour conduire un **Atelier FVA USA**, selon les principes Lean :

> Identifier les activités VA (Value Added), NNVA (Necessary Non-Value Added), NVA (Non-Value Added)  
> et mesurer l’impact de chaque étape sur l’accuracy.

---

## 2. Compétences visées

- Analyse FVA (Forecast Value Added)  
- Identification activités Lean  
- Standardisation processus prévision  
- Détection override destructeur de valeur  
- Recommandation S&OP basée sur la data  
- Synthèse pour direction Supply Chain  

---

## 3. Dataset

📂 Dataset recommandé :  
`datasets/novfood_case_studies/S6_1_FVA_VitalMeal_USA.csv`


---

## 4. Travail demandé — Étapes détaillées

---

### 🔹 Étape 1 — Calculer l’accuracy à chaque étape

Pour chaque SKU, pour chaque période :

\[
\text{MAPE} = \frac{|Forecast - Actual|}{Actual}
\]

À calculer pour :

- Statistical Forecast  
- Sales Override  
- Marketing Override  
- Finance Override  
- Consensus Forecast

📌 **Question 1 : quelles étapes améliorent réellement l’accuracy ?**

---

### 🔹 Étape 2 — Identifier les étapes destructrices de valeur

À partir des MAPE :

- si l’override **augmente** l’erreur → NVA  
- si l’override est **neutre** → NNVA  
- si l’override **diminue** l’erreur → VA  

📌 **Question 2 : quelles équipes détruisent le plus la valeur du processus forecast ?**

---

### 🔹 Étape 3 — Mesurer l’impact global du processus

Pour chaque étape :

- calcul de l’impact moyen sur l’erreur  
- impact par catégorie :
  - SKU à forte rotation,  
  - promos,  
  - innovations.  

📌 **Question 3 : quelle étape génère la plus grande dégradation du MAPE global ?**

---

### 🔹 Étape 4 — Analyse Lean du processus

Classer chaque étape en :

- VA — améliore l’accuracy  
- NNVA — nécessaire mais non créateur de valeur  
- NVA — supprime la valeur (à éliminer)

📌 **Question 4 : quelle proportion du processus est NVA ?**

---

### 🔹 Étape 5 — Recommandations de redesign du processus

Présenter des actions Lean pour :

- réduire la multiplicité des overrides,  
- standardiser les inputs Sales,  
- limiter les sur-optimismes,  
- automatiser certaines décisions,  
- renforcer l’autorité du Demand Planner.

📌 **Question 5 : proposez 5 actions concrètes de redesign.**

---

### 🔹 Étape 6 — Synthèse PowerPoint pour VP Supply Chain USA

Rédiger une note (12–15 lignes) :

- résultats FVA,  
- étapes NVA à éliminer,  
- redesign proposé,  
- bénéfices attendus :
  - réduction MAPE,  
  - réduction effort manuel,  
  - accélération cycle S&OP,  
  - meilleure gouvernance.

📌 **Question 6 : rédigez la synthèse officielle à présenter en comité S&OP.**

---

## 5. Livrables attendus

- Tableau MAPE par étape  
- Diagrammes FVA  
- Synthèse Lean VA/NNVA/NVA  
- Plan de redesign  
- Note S&OP (12–15 lignes)  

---

## 6. Critères d’évaluation

- Pertinence FVA  
- Analyse Lean cohérente  
- Recommandation réaliste  
- Capacité à réduire le bruit prévisionnel  
- Vision S&OP claire  

---

## 7. Extensions (premium)

- Modélisation "noise reduction"  
- Override threshold automatique  
- Gouvernance S&OP Data-Driven  
- Dashboard FVA (Power BI)  
- Simulation “process future state”  

---
