# Cas 8.1 — Détection d’un biais dans un modèle promotionnel (Brésil)  
AI Ethics, transparence & gouvernance — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

NOVAFOOD LATAM utilise un **modèle Machine Learning promotionnel** (XGBoost) pour prédire l’impact des promotions VitalMeal & FreshBite sur le marché brésilien.

Cependant, lors de la dernière revue trimestrielle, l’équipe Data remarque plusieurs signaux suspects :

- certaines enseignes sont systématiquement sur-estimées,  
- certaines régions (Nordeste) sont sous-estimées malgré forte croissance,  
- les promotions digitales semblent mieux “prédictibles” que les promotions en magasin,  
- des biais apparaissent lors de campagnes multi-canal.

La direction LATAM demande un **audit éthique complet du modèle ML** afin de :

1. détecter les biais,  
2. comprendre leur origine,  
3. mesurer leur impact business,  
4. proposer des actions correctives,  
5. produire un rapport auditable pour la gouvernance IA.

Vous êtes chargé de mener cet audit.

---

## 2. Compétences visées

- Détection de biais algorithmique  
- Analyse éthique d’un modèle ML  
- ML explainability (SHAP, feature importance)  
- Fairness metrics  
- Data governance & process governance  
- Communication éthique & transparente  

---

## 3. Dataset

📂 Dataset  :  
`datasets/novfood_case_studies/S8_1_Biais_Model_Promo_BR.csv`

Colonnes :

- `Region`
- `Retailer`
- `Channel` (Store / Digital / Omni)
- `Promo_Discount`
- `Promo_Type` (Display / Digital / Store / Multi)
- `Traffic`
- `Historical_Lift`
- `Predicted_Lift`
- `Actual_Lift`
- `Error`
- `Ethnicity_Index` (pour analyse géographique et socio-économique)
- `Income_Index`
- `Population_Density`

---

## 4. Travail demandé — Étapes détaillées

---

# 🔵 **Étape 1 — Analyse des erreurs par segment**

Analyser l’erreur :

\[
Error = Predicted\_Lift - Actual\_Lift
\]

Comparer :

- par région (Sudeste, Norte, Nordeste…)  
- par retailer  
- par canal (Digital vs Store vs Omni)  
- par type de promotion  

📌 **Question 1 : quels segments montrent le plus fort biais (sur/sous estimation) ?**

---

# 🔵 **Étape 2 — Détection de biais via fairness metrics**

Calculer :

- **Mean Prediction Difference** entre régions  
- **Group Error Ratio**  
- **Disparate Impact Score** (DIS)  
- **Balanced Error Rate** par retailer

Exemple :

\[
DIS = \frac{\text{Pr}(Prediction=high|Region=A)}{\text{Pr}(Prediction=high|Region=B)}
\]

📌 **Question 2 : quel indicateur fairness confirme l’existence d’un biais ?**

---

# 🔵 **Étape 3 — Analyse explicable (Explainability)**

Utiliser :

- Feature importance,  
- SHAP values.

Objectif :

- comprendre quelles variables influencent le plus les prédictions,  
- identifier les variables qui créent une disparité systémique.

📌 **Question 3 : quelle feature est responsable du déséquilibre régional ?**

---

# 🔵 **Étape 4 — Origines du biais**

Analyser les sources possibles :

- données historiques non représentatives,  
- surreprésentation d’enseignes du Sudeste,  
- manque de données Nordeste,  
- poids trop élevé des promotions digitales,  
- saisonnalité asymétrique entre régions.

📌 **Question 4 : listez les causes racines du biais.**

---

# 🔵 **Étape 5 — Correction (Mitigation Plan)**

Proposer des corrections :

- rebalancing des échantillons,  
- ré-entraînement du modèle,  
- pondération ajustée,  
- création de features région-specific,  
- fairness constraints (Equalized Odds / Calibration).

📌 **Question 5 : quelles 5 actions correctives doivent être appliquées ?**

---

# 🔵 **Étape 6 — Rapport de gouvernance IA**

Rédiger une note synthétique (10–15 lignes) incluant :

- le type de biais détecté,  
- l’impact sur la prévision promotionnelle,  
- les conséquences business (budget promo, erreurs MAPE, ruptures),  
- les risques juridiques / réputation,  
- les actions correctives,  
- le plan de monitoring trimestriel.  

📌 **Question 6 : rédigez le rapport IA final pour la Direction LATAM.**

---

## 5. Livrables attendus

- Matrice des erreurs par segment  
- Calcul fairness complet  
- Graphiques SHAP  
- Liste des biais + causes racines  
- Plan de mitigation  
- Rapport IA complet (PDF/MD)  

---

## 6. Critères d’évaluation

- Rigueur dans la détection du biais  
- Analyse statistique cohérente  
- Explication claire via SHAP  
- Actions correctives réalistes  
- Qualité du rapport final  

---

## 7. Extensions (niveau expert)

- Déploiement d’un **Fairness Dashboard** en Power BI  
- Mise en place d’une gouvernance IA trimestrielle (AI board)  
- Monitoring automatique des dérives du modèle  
- Intégration fairness dans SAP IBP ou Oracle DMC  
- Audit cross-pays (Brésil → Mexique → Maroc)  

---
