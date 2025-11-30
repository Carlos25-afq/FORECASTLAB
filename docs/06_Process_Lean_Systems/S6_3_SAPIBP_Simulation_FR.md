# Cas 6.3 — Simulation SAP IBP Francia  
Paramétrage complet du module Demand (DP) dans SAP Integrated Business Planning  
NOVAFOOD GLOBAL — Simulation France

---

## 1. Résumé du cas

La division **NOVAFOOD France** souhaite améliorer la qualité du processus prévisionnel en migrant progressivement ses activités vers **SAP IBP Demand**.  
Elle doit configurer :

- les **time profiles**,  
- les **Master Data Types (MDT)**,  
- les **Planning Areas**,  
- les **Key Figures**,  
- les **Forecast Models**,  
- les **Planning Operators**,  
- les **Job Schedules**.

Vous êtes chargé de réaliser une **simulation complète** de configuration SAP IBP pour construire :

1. un Planning Area conforme au standard NOVAFOOD,  
2. un modèle de forecast (Holt-Winters ou Auto-Model) adapté à FreshBite & NutriBox,  
3. un plan d'exécution complet (operators sequence),  
4. un script d'automatisation de la mise à jour 24h,  
5. un jeu de tests (validation des key figures, des agrégations et des outputs).

L’objectif est d’aligner NOVAFOOD France sur les best practices SAP & Lean Forecasting.

---

## 2. Compétences visées

- Construction d’une **Planning Area**  
- Définition des **Key Figures** et des paramètres  
- Paramétrage des **forecast models** dans SAP IBP Demand  
- Pilotage et exécution des **Planning Operators**  
- Gestion des **time profiles**, MDT et hiérarchies  
- Architecture système et logique S&OP intégrée  
- Pilotage d’un cycle complet DP → Consensus → S&OP

---

## 3. Contexte NOVAFOOD — Scope France

Gammes concernées :

- **FreshBite** (plats végétariens premium)
- **NutriBox** (nutrition active)
- **EcoPure** (eau minérale premium)
- Horizon prévision : **24 mois**
- Granularité : **Hebdomadaire**
- Stock & logistique intégrés à la zone EU

---

## 4. Travail demandé — Étapes détaillées

---

# 🔵 **Étape 1 — Définition du Time Profile SAP IBP**

Créer un **Time Profile** structuré pour la France :

- Level 1 : Month  
- Level 2 : Week  
- Level 3 : Day  
- Attributes recommandés :
  - Fiscal Year
  - ISO Week
  - Week of Month
  - Last Day of Month Indicator

📌 **Question 1 : quels attributs du Time Profile sont critiques pour NOVAFOOD France ?**

---

# 🔵 **Étape 2 — Définition des Master Data Types (MDT)**

MDT obligatoires :

1. **PRODUCT**  
2. **LOCATION**  
3. **CUSTOMER** (optionnel pour retail / e-commerce)  
4. **PRODLOC** (combinaison Produit × Lieu)  
5. **TIME** (lié au Time Profile)  
6. **CUSTPROD** (si besoin granularité client)

Champs suggérés pour PRODLOC :

- Product ID  
- Location ID  
- ABC class  
- Shelf Life  
- Safety Days  
- Transportation Group  
- DP Segment  

📌 **Question 2 : quelles colonnes ajouter au MDT PRODLOC pour modéliser FreshBite ?**

---

# 🔵 **Étape 3 — Construction de la Planning Area**

Planning Area recommandée : **PA_NOVFOOD_FR**

Composants à définir :

- Time Profile  
- MDTs  
- Key Figures  
- Planning Levels  
- Attributes constants  
- Master Data Types attributes  
- Aggregation levels

📌 **Question 3 : quelles Key Figures doivent être agrégées par défaut ?**

---

# 🔵 **Étape 4 — Définition des Key Figures (KFs)**

Liste recommandée :

### 🔹 Prévision & erreurs
- `STAT_FCST`  
- `SALES_OVERRIDE`  
- `MARKETING_OVERRIDE`  
- `FINAL_FCST`  
- `ERROR_ABS`  
- `MAPE`  
- `BIAS`

### 🔹 Supply Planning (préparation S&OP)
- `INVENTORY_TARGET`  
- `SAFETY_STOCK`  
- `SUPPLY_PLAN`

### 🔹 Promo / évènements
- `PROMO_LIFT`  
- `EVENT_FLAG`

### 🔹 Data POS (future integration)
- `POS_SALES`  
- `POS_CORRECTED`

📌 **Question 4 : quelles Key Figures sont nécessaires pour un consensus forecast robuste ?**

---

# 🔵 **Étape 5 — Configuration du Forecast Model**

Pour FreshBite & NutriBox France :

📌 **Modèle recommandé dans SAP IBP : Auto-Model**  
Capable d'identifier automatiquement si la série :

- suit Holt-Winters,  
- suit Single Exponential,  
- suit Double Exponential,  
- suit ARIMA-like patterns.

### Paramètres recommandés :

- Horizon : 24 mois  
- Granularité : Week  
- Outlier correction : ON  
- Intermittent smoothing : ON (NutriBox E-commerce)  
- Damping trend : 0.80  
- Seasonality detection : Auto  
- Alpha / Beta / Gamma : Auto-tuned  

📌 **Question 5 : pourquoi l’Auto-Model est-il mieux que Holt-Winters dans ce contexte ?**

---

# 🔵 **Étape 6 — Planning Operators Sequence**

Créer un **job chain** complet :

1. **Load Master Data**  
2. **Load Key Figures**  
3. **Statistical Forecast Run**  
4. **Promotion & Event Adjustment**  
5. **Final Forecast Aggregation**  
6. **Write Back to Planning Area**  
7. **Publish to S&OP**  

📌 **Question 6 : quel operator doit s'exécuter automatiquement après le Statistical Forecast ?**

---

# 🔵 **Étape 7 — Job Scheduling**

Planification recommandée :

- Stat. Forecast → tous les jours à **03h00**  
- Promo Injection → **03h15**  
- Demand Sensing → **toutes les 3 heures**  
- S&OP Publish → **vendredi 17h00**

📌 **Question 7 : pourquoi le Stat Forecast doit-il tourner avant 04h00 ?**

---

# 🔵 **Étape 8 — Pipeline d’automatisation**

Automatiser (pseudo-code) :

```yaml
trigger: daily
steps:
  - run: LoadMasterData
  - run: LoadKeyFigures
  - run: StatisticalForecast
  - run: PromoAdjust
  - run: ConsensusAggregation
  - run: PublishToSOP


📌 Question 8 : quel contrôle qualité doit être fait avant l'étape PublishToSOP ?

🔵 Étape 9 — Validation & Tests

Tests obligatoires :

cohérence Time Profile

cohérence PRODLOC (matching 100%)

validation erreurs extrêmes corrigées

comparaison modèles Auto vs Holt-Winters

cohérence agrégation Bottom → Top

📌 Question 9 : comment valider la qualité du Time Profile ?

🔵 Étape 10 — Recommandation finale pour NOVAFOOD France

Rédiger une synthèse 12–15 lignes :

bénéfices du modèle SAP IBP

stabilité du consensus forecast

réduction MAPE

suppression overrides inutiles

rapidité de consolidation

montée en maturité S&OP France

📌 Question 10 : rédigez la recommandation complète.

5. Livrables attendus

Configuration complète écrite

Planning Area détaillée

Key Figures catalog

Operators sequence

Job Flow document

Recommandation finale

6. Critères d'évaluation

Cohérence Planning Area

Key Figures pertinentes

Operators sequence logique

Qualité de la recommandation S&OP

Respect SAP IBP Best Practices

7. Extensions (niveau expert)

Ajout module Demand Sensing

Intégration POS Retailers France

Paramétrage multi-pays (Europe)

Extension SAP IBP → ORACLE fusion

Forecasting + ML dans un Planning Operator