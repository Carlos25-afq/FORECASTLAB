# Cas 4.1 — Élasticité prix NutriBox Maroc  
Modèle causal complet : régression multiple, élasticités et simulations commerciales  
NOVAFOOD GLOBAL — Advanced Causal Forecasting

---

## 1. Résumé du cas

NutriBox est une gamme stratégique pour NOVAFOOD GLOBAL au Maroc, un marché en forte croissance mais très sensible aux prix.  
Les ventes y sont influencées par trois facteurs critiques :

- le **prix facial** en rayon,
- l’intensité des **promotions**,
- la saisonnalité culturelle, notamment le **Ramadan**.

La Direction Commerciale Maroc souhaite mieux comprendre :

1. Comment les ventes réagissent aux **variations de prix** (élasticité prix).  
2. Quel est l’impact réel des **promotions** (élasticité promotionnelle).  
3. Quels scénarios prix/promo maximisent volume, revenu ou marge.  
4. Quelles recommandations opérationnelles apporter au S&OP Maroc.

En tant que **Demand Planner Maroc**, votre mission est de :

- construire un **modèle causal robuste** (régression multiple),  
- estimer les **élasticités**,  
- simuler plusieurs **scénarios business**,  
- fournir une **recommandation structurée** pour les arbitrages prix/promo.

---

## 2. Compétences visées

Ce cas développe les compétences clés d’un Demand Planner avancé :

### 📊 Analyse statistique & causalité
- Régression multiple (OLS)
- Lecture et interprétation des coefficients
- Détection multicolinéarité (VIF)
- Test de significativité (p-value, t-statistics)
- Validation statistique du modèle (R², R² ajusté, résidus)

### 💼 Analyse business
- Compréhension des élasticités prix et promo
- Analyse du comportement consommateur
- Traduction des résultats statistiques en recommandations business

### 🔮 Simulation & stratégie commerciale
- Projection du volume en fonction d’un changement de prix
- Simulation de scénarios promotionnels
- Optimisation du revenu / marge / volume

### 🧠 Compétences S&OP
- Construction d’une recommandation claire pour la Direction Commerciale
- Reformulation des résultats pour une audience non technique

---

## 3. Contexte NOVAFOOD — NutriBox Maroc

Au Maroc, NutriBox est présent :

- en grande distribution (Carrefour, Marjane),
- en proximité (BIM, Label'Vie),
- dans certaines marketplaces e-commerce.

Caractéristiques marché :

- Sensibilité prix élevée selon les catégories,
- Impact fort du Ramadan (pic de consommation),
- Promotions agressives des concurrents locaux,
- Inflation alimentaire fluctuante.

Données disponibles sur **36 mois** :

- prix moyen mensuel,
- intensité promo,
- volume mensuel NutriBox,
- variable Ramadan.

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S4_1_NutriBox_Maroc_Elasticity.csv`


---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Analyse exploratoire (EDA)

1. Visualiser l’évolution :
   - des ventes (`Volume`)
   - du prix (`Price`)
   - de la promotion (`PromoIntensity`)
2. Corrélation simple :
   - Price vs Volume  
   - Promo vs Volume  
3. Détection saison Ramadan.

📌 **Question 1 :**  
Décrivez en 5–7 lignes les tendances observées : prix, promo, saison, relation volume.

---

### Étape 2 — Construction du modèle causal

Construire un modèle de type :

\[
Volume = \beta_0 + \beta_1 Price + \beta_2 Promo + \beta_3 Ramadan + \epsilon
\]

Via Excel, Python ou R.

Points à vérifier :

- Significativité statistique (p-value < 0.05)
- Signe des coefficients (Price négatif / Promo positif)
- Multicolinéarité (VIF < 5 idéalement)
- Analyse des résidus

📌 **Question 2 :**  
Quel est le coefficient associé au prix ? Interprétation en langage simple.

---

### Étape 3 — Calcul des élasticités

Calculer :

\[
Elasticité\_Prix = \beta_1 \times \frac{Price}{Volume}
\]

\[
Elasticité\_Promotion = \beta_2 \times \frac{Promo}{Volume}
\]

📌 **Question 3 :**  
NutriBox Maroc est-il **élasique**, **inélastique**, ou **très sensible** au prix ?

---

### Étape 4 — Simulation de scénarios

Simuler les scénarios suivants :

#### **Scénario A : +3% de prix → Volume ?**
#### **Scénario B : Promotion 20% → Volume ?**
#### **Scénario C : Ramadan + Promo légère → Volume ?**
#### **Scénario D : Faible prix + forte promo → Volume + Marge ?**

Écrire les résultats dans un tableau clair.

📌 **Question 4 :**  
Quel scénario maximise le **revenu** ? Le **volume** ? La **marge** ?

---

### Étape 5 — Recommandations S&OP Maroc

Rédiger une note pour :

- orienter la stratégie promo/prix,
- alerter sur les risques (volume, marge),
- intégrer Ramadan dans les prévisions,
- proposer un plan d’action.

📌 **Question 5 :**  
Rédigez une note S&OP (10 lignes) pour la Direction Commerciale Maroc.

---

## 6. Livrables attendus

- Notebook Python / Excel complet
- Matrice de corrélation
- Résultats OLS
- Élasticité prix & promo
- Tableau de simulations
- Note S&OP Maroc

---

## 7. Critères d’évaluation

- Qualité de l’analyse exploratoire
- Robustesse du modèle causal
- Interprétation correcte des coefficients
- Fiabilité des simulations
- Pertinence business des recommandations
- Clarté de la note S&OP

---

## 8. Extensions (niveau expert)

- Modèle SARIMAX (intégration météo ou CPI alimentaire)
- Modèle log-log (élasticités constantes)
- Modèle avec rupture structurelle (avant/après inflation)
- Modèle conjoint prix + cannibalisation entre gammes
- Approche ML : Random Forest Regressor + Shapley Values

---
