# Cas 6.2 — DMAIC : Réduction du MAPE FreshBite Europe  
Méthodologie Lean Six Sigma appliquée au Forecasting — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

La gamme **FreshBite Europe** (plats végétariens premium) connaît depuis 18 mois un :

- MAPE moyen : **28%**  
- Biais moyen : **+12%** (forecast trop optimiste)  
- Erreurs extrêmes : pics > 60% lors de promotions non anticipées  
- Variabilité entre pays (FR, DE, ES, IT)

La Direction S&OP Europe demande un **DMAIC complet** pour :

- identifier les causes racines du mauvais forecasting,
- éliminer le bruit prévisionnel,
- stabiliser la prévision,
- créer un processus robuste, piloté par la data.

Vous êtes le **Demand Planner Europe** chargé de mener le projet.

---

## 2. Compétences visées

- Application complète DMAIC au forecasting  
- Analyse MAPE, biais, extrêmes, variabilité  
- Construction diagramme Ishikawa / Fishbone  
- Identification causes racines par data  
- Définition d’un process futur (to-be)  
- Gouvernance S&OP  
- Réduction bruit / augmentation précision  

---

## 3. Dataset

📂 Dataset  :  
`datasets/novfood_case_studies/S6_2_DMAIC_FreshBite_EU.csv`

Variables :

- `Country`
- `SKU`
- `Month`
- `Forecast`
- `Actual`
- `Promo_Flag`
- `Distribution_Weighted`
- `Temperature_Index`
- `Event_Type`
- `Error_Month`
- `MAPE`
- `Bias`

---

## 4. Travail demandé — DMAIC complet

---

# 🔵 **PHASE D — DEFINE**

### Étape D1 — Définir le problème

Le MAPE FreshBite Europe dépasse 28% → trop élevé pour une gamme premium.

📌 **Question D1 : rédigez une phrase “problem statement” claire et mesurable.**

---

### Étape D2 — Définir les objectifs

Objectifs DMAIC :

- MAPE cible < 18%  
- Biais < 5%  
- Réduction erreurs extrêmes  
- Prévision plus stable pour S&OP + Production  

📌 **Question D2 : formulez 3 objectifs SMART.**

---

### Étape D3 — Délimiter le périmètre (scope)

Pays inclus : FR, DE, ES, IT.  
Pays exclus : marchés mineurs.

📌 **Question D3 : listez les exclusions / contraintes.**

---

---

# 🔵 **PHASE M — MEASURE**

### Étape M1 — Mesurer les erreurs actuelles

Calcul de :

- MAPE global & par pays  
- Biais moyen  
- Distribution des erreurs  
- Top 20 SKU les plus volatils  
- Impact des promos

📌 **Question M1 : quelles sont les 3 sources principales d’erreur mesurées ?**

---

### Étape M2 — Visualisation

Graphiques recommandés :

- forecast vs actuals par pays  
- erreurs extrêmes  
- heatmap MAPE par pays/SKU  
- histogramme des erreurs

📌 **Question M2 : quelles visualisations révèlent les patterns les plus critiques ?**

---

---

# 🔵 **PHASE A — ANALYZE**

### Étape A1 — Analyse Ishikawa

Branches possibles :

- Méthodes : modèles inadaptés  
- Data : MDM incorrect, promos manquantes  
- Process : overrides excessifs  
- Machine : SAP IBP mal paramétré  
- Milieu : météo, événements  
- Main-d’œuvre : Sales optimistes  

📌 **Question A1 : quelles sont les causes racines identifiées ?**

---

### Étape A2 — Validation statistique

Tests possibles :

- corrélation erreur ↔ promo  
- erreur ↔ météo extrême  
- erreur ↔ nouveaux SKU  
- erreur ↔ manque distribution  
- erreur ↔ overrides Sales  

📌 **Question A2 : quelle cause explique le plus la variabilité ?**

---

---

# 🔵 **PHASE I — IMPROVE**

### Étape I1 — Construire les solutions prioritaires

Exemples :

- appliquer des modèles Holt-Winters plus robustes,  
- intégrer météo & distribution dans le modèle causal,  
- limiter overrides à ±8%,  
- créer un formulaire Sales normalisé,  
- activer un demand sensing 48h durant les promos.

📌 **Question I1 : listez 5 solutions concrètes à implémenter.**

---

### Étape I2 — Simulation des gains

Calculer :

- MAPE avant/après  
- Biais avant/après  
- Réduction erreurs extrêmes  
- Gains pour la production & la logistique  

📌 **Question I2 : quel est le gain MAPE estimé après amélioration ?**

---

---

# 🔵 **PHASE C — CONTROL**

### Étape C1 — Mettre en place la gouvernance

Actions recommandées :

- comité forecast bi-hebdomadaire,  
- suivi du biais obligatoire,  
- tableau de bord FVA Europe,  
- seuil override automatique,  
- revue mensuelle accuracy.

📌 **Question C1 : proposez un plan de contrôle mensuel détaillé.**

---

### Étape C2 — Standardisation

- template forecast uniformisé,  
- paramétrage SAP IBP harmonisé,  
- documentation complète “forecasting playbook” Europe.

📌 **Question C2 : quelles 3 procédures doivent être standardisées ?**

---

---

## 5. Livrables attendus

- DMAIC complet (5 phases)  
- Tableau erreurs détaillé  
- Diagramme Ishikawa (PDF ou PNG)  
- Plan d’amélioration (solutions priorisées)  
- Tableaux de comparaison avant/après  
- Plan de contrôle (Control Plan)  

---

## 6. Critères d’évaluation

- Pertinence des causes racines  
- Solutions alignées modèle & process  
- Impact mesurable  
- Logique Lean solide  
- Cohérence S&OP  

---

## 7. Extensions (niveau expert)

- Process “future state” complet  
- Automatisation via SAP IBP / Oracle  
- Override threshold dynamique  
- Contrôle statique vs adaptatif  
- Segmentation forecastability FreshBite  

---
