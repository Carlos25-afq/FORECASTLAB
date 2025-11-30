# Cas 4.4 — Cannibalisation entre FreshBite Classic et FreshBite Zero  
Modèle causal multi-produit, élasticité croisée et analyse d’impact  
NOVAFOOD GLOBAL — Cross-Elasticity & Portfolio Interaction Modeling

---

## 1. Résumé du cas

FreshBite Classic (FBC) et FreshBite Zero (FBZ) sont deux produits leaders de NOVAFOOD dans la catégorie “Healthy Snacks”.

En 2024–2025, l’entreprise observe :

- une croissance modérée de FBC,
- une forte croissance de FBZ,
- mais un **ralentissement anormal** de FBC dans certains pays.

Le Directeur Marketing suspecte un phénomène de **cannibalisation interne** :  
la croissance de FBZ se ferait au détriment de FBC.

Votre rôle, en tant que **Global Demand Planner FreshBite**, est de :

1. Construire un **modèle causal multi-produit**  
2. Estimer les **élasticités croisées** (cross-price, cross-volume)  
3. Quantifier le niveau de cannibalisation  
4. Simuler différents scénarios prix / promo  
5. Fournir une **recommandation de gestion du portefeuille** pour le S&OP Global

Ce cas est critique : il conditionne les décisions marketing, supply et financières.

---

## 2. Compétences visées

### 📊 Analyse statistique avancée
- Modèle multivarié Volume_FBC ~ Volume_FBZ / Price_FBC / Price_FBZ  
- Élasticités croisées  
- Effet de substitution  

### 📉 Analyse business
- Impact sur portefeuille  
- Effet net vs effet brut  
- Risques de sur-favorisation d’un SKU  

### 🎯 Stratégie commerciale
- Construction d’un portefeuille cohérent  
- Arbitrage entre croissance totale vs croissance cannibalisante  

---

## 3. Contexte NOVAFOOD — FreshBite Classic & Zero

Caractéristiques des deux produits :

| Critère | FreshBite Classic | FreshBite Zero |
|--------|------------------|----------------|
| Positionnement | Standard | Sans sucre |
| Audience | Grand public | Healthy premium |
| Prix | Modéré | +10–15% |
| Sensibilité promo | Moyenne | Faible |
| Croissance | Stable | Forte |

Relations possibles :

- **Substitution** : FBZ remplace FBC  
- **Complémentarité** : certains clients achètent les deux  
- **Cannibalisation** : croissance FBZ → baisse FBC  
- **Émergence** : FBZ attire de nouveaux consommateurs (non cannibalisants)

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S4_4_FreshBite_Cannibalisation.csv`


---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Analyse exploratoire

1. Tracer :
   - FBC_Volume
   - FBZ_Volume
2. Étudier la corrélation entre les deux volumes
3. Vérifier si FBC diminue quand FBZ augmente

📌 **Question 1 :**  
Les premières observations suggèrent-elles une cannibalisation ? Expliquez.

---

### Étape 2 — Modèle causal multi-produit

Modèle recommandé :

\[
FBC\_Volume = \beta_0 + \beta_1 Price\_{FBC} + \beta_2 Price\_{FBZ} + \beta_3 FBZ\_Volume + \beta_4 Season + \epsilon
\]

Points clés :

- β₃ < 0 = substituabilité / cannibalisation  
- β₂ > 0 = cross-price effect (substitution prix)  
- β₂ < 0 = complémentarité  

📌 **Question 2 :**  
Quel coefficient confirme le mieux la cannibalisation ?

---

### Étape 3 — Élasticités croisées

Élasticité croisée prix :

\[
Ex = \beta_2 \times \frac{Price_{FBZ}}{Volume_{FBC}}
\]

Élasticité croisée volume :

\[
Ev = \beta_3 \times \frac{FBZ\_Volume}{FBC\_Volume}
\]

📌 **Question 3 :**  
FreshBite Zero a-t-il un impact faible, modéré ou fort sur FreshBite Classic ?

---

### Étape 4 — Simulation de scénarios

Simuler :

#### **Scénario A : Promo -10% sur FBZ → impact sur FBC ?**  
#### **Scénario B : Hausse prix FBC +5%**  
#### **Scénario C : Promo combinée FBC + FBZ (bundle)**  
#### **Scénario D : Retrait d’une promotion FBZ**  

À chaque scénario, calculer :

- Variation FBC  
- Variation FBZ  
- Impact net vs effet cannibalisant  
- Impact sur le **portefeuille global FreshBite**

📌 **Question 4 :**  
Quel scénario maximise les ventes totales du portefeuille FreshBite ?

---

### Étape 5 — Analyse de cannibalisation nette

Calculer :

\[
Cannibalisation = \frac{Perte\_FBC\_due\_à\_FBZ}{Gain\_FBZ\_observé}
\]

Interprétation :

- < 20% → cannibalisation faible  
- 20–50% → modérée  
- > 50% → forte  
- > 100% → cannibalisation destructrice  

📌 **Question 5 :**  
Quel est le niveau de cannibalisation observé ? Implications business ?

---

### Étape 6 — Recommandation S&OP

Rédiger une synthèse :

- impact du lancement de FBZ sur Classic  
- arbitrages commerciaux  
- stratégies anti-cannibalisation :
  - segmentation des promos  
  - différenciation des packagings  
  - pricing intelligent  
  - calendriers promo séparés  

📌 **Question 6 :**  
Rédigez une note S&OP (8–10 lignes) à la Direction Global FreshBite.

---

## 6. Livrables attendus

- Notebook Python / Excel avec :
  - modèle multivarié  
  - élasticités croisées  
  - scénarios  
- Graphiques :
  - volumes  
  - effet promo  
  - effet croisé  
- Note S&OP claire et synthétique  

---

## 7. Critères d’évaluation

- Qualité du modèle  
- Interprétation correcte des elasticités  
- Réalisme des scénarios  
- Recommandation business pertinente  
- Cohérence S&OP  

---

## 8. Extensions (niveau expert)

- Modèle log-log (élasticités stables)  
- Random Forest Regressor + SHAP pour interactions produit  
- Modèle vectoriel (VAR) FBC/FBZ  
- Modèle bayésien cannibalisation  
- Analyse multi-country (FR, DE, VN, BR)  

---
