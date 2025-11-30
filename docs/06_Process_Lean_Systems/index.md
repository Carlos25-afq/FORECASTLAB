# 06 — Process, Lean Six Sigma & Planning Systems  
NOVAFOOD GLOBAL — Gouvernance, Excellence Opérationnelle & Intégration Systèmes (SAP, Oracle, Sofco, OMP)

Un Demand Planner performant n’est pas seulement un expert en modèles ; il est le **pilote du processus de planification**.  
La Section 6 explique comment NOVAFOOD structure son processus, améliore l’accuracy via Lean Six Sigma, et intègre les prévisions dans les systèmes de planification (APS).

---

# 🎯 Objectifs de la section

À la fin de cette section, vous serez capable de :

- Comprendre et cartographier le processus de prévision NOVAFOOD  
- Appliquer Lean et Six Sigma pour améliorer l’accuracy  
- Utiliser les méthodologies DMAIC & DFSS  
- Identifier les activités à valeur ajoutée via **FVA**  
- Comprendre l’architecture des systèmes APS (SAP IBP, Oracle, Sofco, OMP)  
- Construire un pipeline complet Power Query → Power BI → APS  
- Déployer une gouvernance forecast robuste

---

# 🧩 1. Processus de prévision NOVAFOOD : la colonne vertébrale

NOVAFOOD suit un processus global standardisé sur 18 pays :

### **Étape 1 : Prévision statistique (Baseline)**
- MA, SES, Holt-Winters  
- ARIMA / ML selon forecastability  
- Génération portfolio modèle par modèle

### **Étape 2 : Enrichissement Sales / Marketing**
- Intégration promotions  
- Insights distributeurs (POS)  
- NPD → quantification early-stage  

### **Étape 3 : Consolidation Finance**
- Atterrissage budgétaire  
- Analyse écart Forecast vs Budget  
- Alignement P&L  

### **Étape 4 : Pré-S&OP**
- Préparation arbitrages  
- Analyse risques & opportunités  
- Gap closing  

### **Étape 5 : Executive S&OP**
- Arbitrages COMEX  
- Décisions Supply (capacité, priorisation)  
- Publication Consensus Forecast  

### **Étape 6 : Intégration APS**
- Envoi forecast vers SAP IBP / Oracle  
- Génération plan appro / prod  

---

# 🧩 2. Lean Forecasting : Éliminer le gaspillage

NOVAFOOD applique les principes Lean afin d’identifier :

- **VA** (Value Added) → améliore l’accuracy  
- **NNVA** (Necessary Non-Value Added) → obligatoire mais inutile  
- **NVA** (Non-Value Added) → à supprimer  

Exemples NOVAFOOD :

| Activité | Catégorie |
|----------|-----------|
| Correction promo par Sales | VA |
| Double saisie Excel → ERP | NVA |
| Analyses distribution | VA |
| Consolidation PowerPoint | NNVA |

Objectif :  
➡️ réduire le bruit, réduire les retards, augmenter la qualité du plan.

---

# 🧩 3. Méthodes Six Sigma — DMAIC & DFSS

## 3.1 DMAIC : Amélioration continue de l’accuracy

### **Define**
- Scope : FreshBite Europe (MAPE trop élevé)  
- VOC : Sales, Supply, Finance → “Forecast non actionnable”  

### **Measure**
- Collecter : FE, MAPE, BIAS, CV  
- Comparer : Baseline vs consensus vs S&OP  

### **Analyze**
- Ishikawa :  
  - Données Sales imprécises  
  - Promotions non documentées  
  - Capacité usine non alignée  
  - Effet météo ignoré  

### **Improve**
- Mise en place d’un calendrier promo unifié  
- Ajout features météo dans baseline  
- Alignement capacités usine  
- Mise en place forecastability scoring  

### **Control**
- Reporting accuracy hebdo  
- KPI S&OP mensuel  
- Ownership local + global  

---

## 3.2 DFSS : Design for Six Sigma (NPD Forecasting)

Appliqué aux lancements FreshBite Vegan.

Étapes :  
- **Identify** → drivers marché  
- **Design** → Looks-Like + diffusion  
- **Optimize** → markov + cannibalisation  
- **Validate** → backtest  
- **Deploy** → diffusion S&OP

---

# 🧩 4. Systèmes APS : SAP IBP, Oracle, Sofco, OMP

### **SAP IBP**
- Modules : IBP for Demand, IBP for Inventory  
- Strengths :  
  - segmentation forecast  
  - interactive dashboards  
  - demand sensing  
  - ML intégré  

### **Oracle Demand Management**
- Strengths :  
  - multi-pays intégré ERP Oracle  
  - forte gestion des promotions  
  - workflows collaboratifs  

### **Sofco (Planning Régional Europe)**
- Strengths :  
  - rapidité  
  - interface intuitive  
  - facilité multi-scénarios  

### **OMP / Blue Yonder**
- Pour les environnements complexes  
- Optimisation réseau + planification supply  

---

# 🧩 5. Pipeline Data → Forecast → APS

Chez NOVAFOOD, un pipeline APS standard est :

1. **Power Query** → ingestion multi-sources (18 pays)  
2. **Power BI / DAX** → calcul KPIs accuracy  
3. **Notebook Python** → modèles avancés  
4. **Export CSV** → fichier APS standardisé  
5. **Upload automatique** via API / batch job  
6. **Validation Supply Planner**  
7. **Intégration dans SAP IBP / Oracle**  

---

# 🧪 CAS PRATIQUES NOVAFOOD

---

## **6.1 : Atelier FVA sur VitalMeal USA**
🎯 Objectif :  
Identifier les étapes du processus qui dégradent le forecast.

Livrables :  
- Matrice FVA complète  
- Analyse VA / NNVA / NVA  
- Plan d’amélioration

---

## **6.2 : DMAIC — réduire le MAPE FreshBite Europe**
🎯 Objectif :  
Conduire un DMAIC complet sur la gamme FreshBite.

Livrables :
- Ishikawa  
- Dashboard accuracy  
- Plan d'action opérationnel

---

## **6.3 : Simulation SAP IBP Francia**
🎯 Objectif :  
Simuler un cycle forecast → APS sous SAP IBP.

Livrables :
- Capture IBP  
- Mapping data  
- Exemple d’alertes

---

## **6.4 : Pipeline Power Query → API → Oracle**
🎯 Objectif :  
Créer un pipeline automatisé complet.

Livrables :
- Script Power Query  
- Script API (Python)  
- Fichier Oracle-ready

---

# 📌 Navigation

- [Section 7 — Demand Sensing & Real-Time Forecasting](../07_Demand_Sensing_RealTime/index.md)  
- [Retour au sommaire FORECASTLAB](../../README.md)

---
