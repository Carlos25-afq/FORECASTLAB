# Cas 3.1 — Prévision NutriBox France sur 36 mois  
NOVAFOOD GLOBAL — Modélisation Holt-Winters & Analyse Saisonnière

---

## 1. Résumé du cas

NutriBox est la gamme de produits “snacking sain” de NOVAFOOD GLOBAL.  
En France, les ventes de NutriBox présentent :

- une **tendance de fond** liée à la croissance du marché,
- une **saisonnalité marquée** (rentrée, fêtes, été),
- des **pics ponctuels** liés aux promotions.

Votre rôle, en tant que **Demand Planner France NutriBox**, est de construire une prévision mensuelle robuste pour les **12 prochains mois**, à partir de **36 mois d’historique**.

L’objectif est de comparer différentes approches, d’expliquer les résultats au S&OP, et de proposer un **forecast actionnable** pour la production et la logistique.

---

## 2. Compétences visées

Ce cas pratique développe les compétences suivantes :

- Analyse de séries temporelles (trend, saisonnalité, résidus)
- Construction d’un modèle Holt-Winters (additif / multiplicatif) dans Excel
- Compréhension du lien entre **bruit** et **signal**
- Lecture critique des prévisions (visuel + métriques d’erreur)
- Capacité à expliquer un forecast à des non-statisticiens (Sales, Supply, Finance)

---

## 3. Contexte NOVAFOOD — NutriBox France

- Marque : **NutriBox**
- Pays : **France**
- Horizon : **36 mois d’historique** (M-36 à M-1), prévision **12 mois** (M à M+11)
- Granularité : **Mensuelle**
- Canal : **Retail + E-commerce agrégés**
- KPI principal : **Volume vendu (en unités)**

Les prévisions NutriBox FR alimentent :

- les plans de production de l’usine France,
- les besoins logistiques des hubs Europe,
- la construction du **Consensus Forecast** en S&OP.

---

## 4. Jeu de données

📂 Fichier cible  :  
`datasets/novfood_case_studies/S3_1_NutriBox_FR_36Mois.csv`

---

## 5. Travail demandé — Étapes détaillées

### Étape 1 — Analyse visuelle de la série

1. Importer les données dans Excel (ou Power BI / Python).  
2. Tracer la série `NutriBox_FR_Demand` sur 36 mois.  
3. Identifier visuellement :
   - tendance (croissante, stable, non linéaire),
   - saisonnalité (mois récurrents haut / bas),
   - anomalies (pics, creux).

📌 **Question 1 :**  
Décrivez la série en 5–7 lignes : tendance, saisonnalité, anomalies.

---

### Étape 2 — Décomposition de la série

1. Construire une **moyenne mobile centrée** (par ex. 12 mois si saisonnalité annuelle).  
2. Extraire :
   - la composante **trend**,  
   - la composante **saison**,  
   - les **résidus**.

📌 **Question 2 :**  
Quelle est la saisonnalité de NutriBox FR ?  
Quels mois sont typiquement les plus forts / les plus faibles ?

---

### Étape 3 — Modèle Holt-Winters additif

1. Initialiser :
   - niveau initial  
   - tendance initiale  
   - facteurs saisonniers  
2. Choisir des valeurs initiales pour les coefficients (α, β, γ), ex. 0,2 / 0,1 / 0,2.  
3. Implémenter Holt-Winters **additif** dans Excel sur la période historique.  
4. Calculer la prévision sur les 12 mois futurs.

📌 **Question 3 :**  
Quelle est la MAPE obtenue sur la période historique pour ce modèle additif ?

---

### Étape 4 — Modèle Holt-Winters multiplicatif

1. Reprendre les mêmes étapes mais avec une version **multiplicative**.  
2. Comparer les résultats :
   - courbes forecast vs actual  
   - erreurs (MAPE, Bias, RMSE)  

📌 **Question 4 :**  
Quel modèle (additif ou multiplicatif) décrit le mieux NutriBox FR ? Pourquoi ?

---

### Étape 5 — Analyse des résidus

1. Tracer les résidus (Actual – Forecast) du meilleur modèle.  
2. Vérifier :
   - absence de pattern clair,  
   - absence de biais systématique,  
   - “randomness” autour de 0.

📌 **Question 5 :**  
Les résidus sont-ils compatibles avec l’hypothèse “bruit aléatoire” ? Expliquez.

---

### Étape 6 — Prévision 12 mois + Narration S&OP

1. Finaliser la prévision à 12 mois.  
2. Préparer une **slide unique** ou une **note** de synthèse pour le S&OP :

Inclure :
- graphique historique + forecast  
- 3–4 messages clés (tendance, saison, risques)  
- principaux risques (promotions lourdes, canicule, nouvelle concurrence)  
- recommandations (capacité, stock, arbitrages)

📌 **Question 6 :**  
Formulez en 8–10 lignes la narration pour le S&OP France.

---

## 6. Livrables attendus

Pour un cas complet niveau “Demand Planner Pro”, les livrables sont :

1. **Fichier Excel** avec :
   - données  
   - décomposition  
   - modèles Holt-Winters additif + multiplicatif  
   - calcul des erreurs  

2. **Graphiques** :
   - Série historique + forecast  
   - Trend + saisonnalité  
   - Résidus  

3. **Note de synthèse** (ou slide S&OP) expliquant :
   - la logique du modèle  
   - la saisonnalité NutriBox FR  
   - le forecast à 12 mois  
   - les risques identifiés  

---

## 7. Critères d’évaluation

- Qualité de l’analyse visuelle et de la décomposition  
- Pertinence du choix de modèle (additif vs multiplicatif)  
- Correctitude des implémentations Excel (formules, cohérence)  
- Qualité des métriques d’erreur calculées (MAPE, Bias, RMSE)  
- Capacité à interpréter les résidus  
- Qualité de la narration S&OP (clarté, orientation décision)  

---

## 8. Extensions (niveau avancé)

Pour aller plus loin :

- Comparer Holt-Winters vs un **ARIMA saisonnier** sous Python / R.  
- Tester plusieurs jeux de paramètres (α, β, γ) et optimiser MAPE.  
- Étendre l’analyse à NutriBox Espagne / Italie et comparer les profils.  
- Simuler un choc externe (ex : canicule ou grève logistique) et mesurer l’impact.  

---
