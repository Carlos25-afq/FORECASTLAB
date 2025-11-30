# Cas 4.2 — Modèle promotionnel VitalMeal Brésil : Analyse d'uplift & optimisation promo  
NOVAFOOD GLOBAL — Promotion Analytics & Causal Impact

---

## 1. Résumé du cas

VitalMeal est une des gammes nutritionnelles les plus vendues de NOVAFOOD au Brésil.  
Le marché brésilien est extrêmement sensible aux promotions :

- 38% des ventes sont réalisées pendant des périodes promo,
- les enseignes utilisent des remises agressives (-20% à -40%),
- les volumes promo perturbent fortement les prévisions.

Le Directeur Commercial Brésil veut répondre à 3 questions critiques :

1. **Quel est le vrai uplift promotionnel ?**  
2. **Quelle part des ventes promo est réellement incrémentale ?**  
3. **Quelles promotions généreront le meilleur ROI dans les 12 prochains mois ?**

En tant que **Demand Planner Brésil**, vous devez :

- construire un **modèle causal pour mesurer l’impact des promotions**,  
- calculer l’uplift incrémental réel,  
- détecter le cannibalisme potentiel,  
- simuler 3 scénarios promotionnels,  
- recommander un **plan promo optimisé** pour le S&OP LATAM.

---

## 2. Compétences visées

### 📊 Analyse promotionnelle avancée
- Incrementality vs volume transféré  
- Mesure de l’effet causal des promotions  
- Modèle avec variables binaires & intensité promo  
- Analyse post-promo dip  
- CausalImpact (Google) ou version Excel

### 🔮 Uplift modeling
- Uplift = Ventes(Promo) – Ventes(Sans Promo)  
- Modèle additif ou multiplicatif  
- Simulation des remises (10%, 20%, 30%, etc.)

### 💼 Compétences commerciales & S&OP
- Définition d’un plan promo rentable  
- Arbitrage entre volume vs marge  
- Interprétation business orientée décision

---

## 3. Contexte NOVAFOOD — VitalMeal Brésil

Les promotions représentent :

- un **drivers clé de pénétration marché**,
- un levier essentiel face aux concurrents locaux,
- un risque de distorsion des prévisions.

Types de promotions observées :

- **Taux de remise** (10%, 20%, 30%)  
- **Bundles** (2+1, 3 pour 2)  
- **Mise en avant magasin** (tête de gondole)  

Échantillon historique disponible :

- 36 mois de données mensuelles VitalMeal Brésil

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S4_2_VitalMeal_Brazil_Promo.csv`


---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Analyse exploratoire

1. Tracer série Volume + Promo_Flag  
2. Identifier :
   - pics liés aux promotions,  
   - éventuels post-promo dips (volume artificiellement bas),  
   - corrélation Prix / Volume / Promo.

📌 **Question 1 :**  
Quels signes indiquent que les promotions distordent la demande ?

---

### Étape 2 — Modèle causal de base

Construire un modèle OLS :

\[
Volume = \beta_0 + \beta_1 Promo\_Depth + \beta_2 Display + \beta_3 Price + \beta_4 Seasonality + \epsilon
\]

📌 **Question 2 :**  
Le coefficient β1 est-il significatif ?  
Quelle est son interprétation business simple ?

---

### Étape 3 — Calcul de l’uplift promotionnel réel

Uplift = Volume(promo) – Volume(scénario sans promo)

Créer deux colonnes :

- `Pred_NoPromo` : prédiction du modèle avec Promo_Flag = 0  
- `Incrementality` = `Volume` – `Pred_NoPromo`

📌 **Question 3 :**  
Quelle proportion des ventes promo de VitalMeal est réellement incrémentale ?

---

### Étape 4 — Détection du post-promo dip

Identifier :

- baisse anormale juste après promo,
- réduction du volume baseline.

📌 **Question 4 :**  
Le post-promo dip est-il présent ? Quel est son impact ?

---

### Étape 5 — Simulation de scénarios promo 2026

Simuler :

#### **A — Promo faible (-10%) / 1 mois**
#### **B — Promo standard (-20%) / 1 mois**
#### **C — Promo agressive (-30%) / 2 mois**
#### **D — Bundle 2+1 sans remise forte**
#### **E — Scénario mix (Promo faible + Display)**

Calculer :

- Volume attendu  
- Volume incrémental  
- Revenu  
- Marge estimée  
- ROI promo

📌 **Question 5 :**  
Quel scénario maximise marge ?  
Quel scénario maximise volume ?

---

### Étape 6 — Recommandation S&OP LATAM

Synthèse à présenter :

- Impact promo  
- Risques de cannibalisme  
- Risque post-promo  
- Recommandation du mix promo 2026

📌 **Question 6 :**  
Rédigez une note S&OP (8–10 lignes) à la Direction LATAM.

---

## 6. Livrables attendus

- Notebook Python / Excel avec :
  - modèle OLS  
  - uplift calculation  
  - simulations promo  
- Graphiques (effet promo et post-promo)  
- Tableau comparatif de scénarios  
- Note S&OP Brésil  

---

## 7. Critères d’évaluation

- Modèle causal correctement construit  
- Mesure correcte de l’incrémentalité  
- Détection pertinente du post-promo dip  
- Simulation business réaliste  
- Qualité de la recommandation S&OP  

---

## 8. Extensions (niveau expert)

- Modèle CausalImpact (Google)  
- Random Forest Regressor pour uplift modeling  
- Cannibalisation : impact des promos VitalMeal sur FreshBite  
- Modèle économétrique : elasticité croisée  
- Optimisation automatique via grid-search des promotions

---
