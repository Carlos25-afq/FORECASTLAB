# Cas 8.2 — Construire un Modèle de Prévision Explicable & Responsable  
Explainable AI (XAI) + Gouvernance + Transparence — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

Pour renforcer la confiance des équipes Sales, Marketing, Finance et S&OP, NOVAFOOD GLOBAL souhaite remplacer ses modèles “boîte noire” (XGBoost, Random Forest, AutoML) par un **modèle explicable** capable de :

- justifier chaque prévision,  
- quantifier l’impact des drivers (prix, météo, distribution…),  
- rendre la prévision auditable (conformité SOX / normes internes),  
- détecter les dérives algorithmique,  
- produire un **forecast responsable** utilisable en comité S&OP.

Vous êtes nommé **Owner IA Responsable** pour :

1. construire un modèle explicable,  
2. générer un rapport de transparence automatisé,  
3. définir les règles de gouvernance IA pour NOVAFOOD,  
4. établir les protocoles de monitorings trimestriels,  
5. assurer la justice et l’absence de biais dans le forecast.

---

## 2. Compétences visées

- Explainable AI (XAI) appliqué au forecasting  
- SHAP, LIME, modèle GAM (Generalized Additive Model)  
- Modélisation transparente (ElasticNet, GAM, Decision Rules)  
- Gouvernance IA (documentation, auditabilité, traçabilité)  
- S&OP Data Governance Framework  
- Détection & mitigation de biais  

---

## 3. Dataset

📂 Dataset :  
`datasets/novfood_case_studies/S8_2_Explainable_Responsible_Model.csv`

Colonnes :

- `SKU`
- `Country`
- `Week`
- `Price`
- `Promo_Flag`
- `Distribution_Weighted`
- `Temperature`
- `Competitor_Price`
- `Historical_Sales`
- `Baseline_Forecast`
- `Actual_Sales`
- `Model_Prediction`
- `SHAP_Contribution_*`
- `Feature_Reliability_Index`

---

## 4. Travail demandé — Étapes détaillées

---

# 🔵 **Étape 1 — Choisir un modèle explicable**

Modèles recommandés pour NOVAFOOD :

### A. **GAM — Generalized Additive Model**
Très lisible, exprime l’impact de chaque variable séparément :

\[
Sales = f_1(Price) + f_2(Temperature) + f_3(Distribution) + f_4(Promo)
\]

### B. **ElasticNet**
- simple,
- contrôlable,
- robuste,
- facile à auditer.

### C. **Decision Rules (RuleFit)**
Exemple :

- *Si Promo = 1 et Temp > 25°C → +18% lift attendu*  
- *Si Distribution < 50% → baisse systématique*

📌 **Question 1 : quel modèle explicable recommandez-vous pour FreshBite France ? Pourquoi ?**

---

# 🔵 **Étape 2 — Génération des SHAP values**

Vous devez :

- calculer l’impact marginal de chaque feature,  
- générer les graphiques SHAP :
  - summary plot,
  - waterfall plot,
  - decision plot.

Pour une semaine donnée :

\[
Forecast = Baseline + \sum SHAP_{i}
\]

📌 **Question 2 : quelle variable a le SHAP moyen le plus élevé (impact majeur) ?**

---

# 🔵 **Étape 3 — Construction d’un Rapport de Transparence (Transparency Report)**

Le rapport doit contenir :

- Description du modèle  
- Justification du choix  
- Drivers principaux (top 5 SHAP)  
- Analyse des risques  
- Limites du modèle  
- Données utilisées  
- Qualité & complétude data  
- Vérifications pré-forecast  
- Historique des modifications  
- Documentation “RAI” (Responsible AI)  

📌 **Question 3 : que doit contenir la section “Limitations du modèle” ?**

---

# 🔵 **Étape 4 — Gouvernance IA (charte interne)**

Définir un cadre structuré :

### A. **Principes**
- transparence  
- auditabilité  
- équité  
- sécurité des données  
- non-discrimination  
- robustesse  

### B. **Acteurs**
- Demand Planner  
- Data Scientist  
- Responsable IA  
- Directeur S&OP  
- DPO / Legal  

### C. **Règles**
- override limité  
- explication obligatoire pour chaque ajustement  
- SHAP généré automatiquement  
- versionning des modèles  

📌 **Question 4 : proposez 4 règles obligatoires pour toute IA de forecasting chez NOVAFOOD.**

---

# 🔵 **Étape 5 — Détection automatique des dérives (model drift)**

Indicateurs :

- Model Drift  
- Data Drift  
- Concept Drift  
- Anomaly Drift  
- Variation SHAP irrégulière  
- MAPE vs baseline  

📌 **Question 5 : comment détecter un “Concept Drift” sur FreshBite EU ?**

---

# 🔵 **Étape 6 — Préparation au Comité S&OP**

Le modèle doit générer :

- Forecast  
- Range (P10/P50/P90)  
- Drivers expliqués  
- Risques  
- Opportunités  

Recommandation format : 📌 Driver #1 : Prix
📌 Driver #2 : Distribution
📌 Driver #3 : Température
📌 Driver #4 : Promo
📌 Driver #5 : Compétition


📌 **Question 6 : rédigez un message explicatif de 10 lignes pour le COMEX.**

---

# 🔵 **Étape 7 — Documentation & Auditabilité**

Documents obligatoires :

- Fiche modèle  
- Version du modèle  
- Paramètres utilisés  
- Résultats de tests  
- Journal des executions  
- Archive des SHAP mensuels  
- Historique de mise à jour  

📌 **Question 7 : que doit contenir un “Audit Log IA” mensuel ?**

---

## 5. Livrables attendus

- Modèle explicable (ElasticNet / GAM / RuleFit)  
- SHAP values + graphiques  
- Transparency Report complet  
- Charte de Gouvernance IA  
- Plan drift monitoring  
- Matrice risques & limites  

---

## 6. Critères d’évaluation

- Clarté de l’explication  
- Pertinence du modèle choisi  
- Robustesse de la gouvernance IA  
- Détection correcte des biais  
- Communication efficace au COMEX  

---

## 7. Extensions (niveau expert)

- Explainable Deep Learning (xLSTM)  
- Dashboard d’explicabilité (Power BI / Looker)  
- Auto-documentation IA  
- Proxy fairness + SHAP fairness  
- Structure RAI multi-pays NOVAFOOD  

---


