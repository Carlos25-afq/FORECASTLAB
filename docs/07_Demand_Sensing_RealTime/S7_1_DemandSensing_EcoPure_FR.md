# Cas 7.1 — Demand Sensing EcoPure France  
Prévision court terme J+1 / J+7 basée sur POS quotidien et météo — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

EcoPure (gamme d’eau minérale premium de NOVAFOOD) connaît une croissance rapide en France.  
La demande est **très sensible** à :

- la météo (température, humidité),
- les promotions locales,
- les week-ends et jours fériés,
- les ventes POS (Point-of-Sale) des enseignes.

L’équipe S&OP France demande désormais un **demand sensing** opérationnel pour :

- recalculer automatiquement la prévision à **H+12**, **H+24**, **J+1**, **J+7**,  
- intégrer des signaux exogènes **POS + Météo**,  
- fournir un forecast court terme robuste pour :
  - la distribution,
  - les flux entre entrepôts,
  - la logistique urbaine,
  - l’optimisation du stock journalier.

Vous êtes le **Demand Planner France** en charge de :

- détecter les signaux faibles,
- construire un modèle court terme,
- simuler différents scénarios météo,
- recommander les ajustements opérationnels journaliers.

---

## 2. Compétences visées

- Analyse POS (Point-of-Sale)  
- Prévision court terme (nowcasting / H+12 / H+24)  
- Intégration signaux faibles (météo, événements locaux)  
- Feature engineering avancé  
- Modèle adaptatif court terme (ETS, Regression courte, RF short-horizon)  
- Mesure du risque de rupture intra-semaine  
- Recommandation logistique journalière  

---

## 3. Dataset

📂 Dataset recommandé :  
`datasets/novfood_case_studies/S7_1_DemandSensing_EcoPure_FR.csv`


---

## 4. Travail demandé — Étapes détaillées

---

### 🔹 Étape 1 — Analyse POS + Météo (exploration)

Pour 6 mois glissants :

1. tracer les POS journaliers,  
2. identifier les patterns météo → demande,  
3. calculer corrélations :
   - POS ↔ température  
   - POS ↔ humidité  
   - POS ↔ jours fériés  
4. détecter :
   - pics anormaux,  
   - ruptures magasin,  
   - promotions non déclarées.

📌 **Question 1 : quelles sont les 3 variables les plus corrélées aux ventes POS ?**

---

### 🔹 Étape 2 — Construction du modèle court terme (J+1)

Modèle recommandé :

\[
Demand_{J+1} = \alpha POS_{J} + \beta Temp_{J+1} + \gamma Promo + \delta Saison + \epsilon
\]

Autres alternatives :

- ETS court terme,
- Random Forest short-horizon,
- Regression glissante sur 30 derniers jours.

📌 **Question 2 : quel modèle J+1 obtient le meilleur MAPE court terme ?**

---

### 🔹 Étape 3 — Forecast adaptatif J+7 (weekly horizon)

Méthode via **features glissantes** :

- POS (lag 1–7),
- Température prévisionnelle (source météo),
- Effets calendaires,
- Promo à venir.

Sorties attendues :

- Forecast J+7 avec bande d’incertitude,  
- Fan chart court terme.

📌 **Question 3 : quelle est la probabilité que la demande dépasse le P90 J+7 ?**

---

### 🔹 Étape 4 — Détection des signaux faibles (anomalies)

Implémenter une détection d’anomalies :

- Z-score,
- isolation forest,
- IQR.

Objectif :

- identifier un pic météo,  
- détection promo non déclarée,  
- signal POS anormal → recalibration immédiate du forecast.

📌 **Question 4 : quels magasins / jours présentent des anomalies POS ?**

---

### 🔹 Étape 5 — Recommandation opérationnelle intra-semaine

Selon :

- le forecast J+1 / J+7,
- la météo,
- le niveau d’inventaire magasin / DC,
- les pics de demande possibles,

Vous devez recommander :

1. transferts entre entrepôts,  
2. réappro magasin prioritaire,  
3. ajustement de la prod (si possible),  
4. ajustement transport quotidien (camions supplémentaires).

📌 **Question 5 : quelle stratégie recommandez-vous pour les 3 prochains jours ?**

---

### 🔹 Étape 6 — Note au Directeur France (10–12 lignes)

Contenu attendu :

- variation versus forecast plan initial,  
- risques identifiés,  
- impact météo,  
- niveaux de stocks critiques,  
- plan d’action opérationnel,  
- recommandations logistiques.

📌 **Question 6 : rédigez la note complète.**

---

## 5. Livrables attendus

- Notebook Python ou Excel  
- Forecast J+1 et J+7  
- Bande d’incertitude (fan chart)  
- Détection anomalie POS  
- Tableau des réappros recommandés  
- Note stratégique prête S&OP  

---

## 6. Critères d’évaluation

- Qualité du modèle court terme  
- Bonne intégration météo  
- Détection anomalies pertinente  
- Recommandation opérationnelle réaliste  
- Présentation claire  

---

## 7. Extensions (niveau expert)

- Demand sensing multi-entrepôts  
- Dashboard temps réel (Power BI streaming dataset)  
- Intégration API météo (OpenWeather)  
- Modèle hybride ML + séries temporelles  
- Simulation transport intra-semaine  

---
