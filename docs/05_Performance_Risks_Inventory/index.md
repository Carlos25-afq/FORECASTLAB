# 05 — Performance, Forecastability, Inventory & Risks  
NOVAFOOD GLOBAL — Accuracy, Variabilité, Stock de Sécurité & Résilience

Cette section explique comment mesurer, interpréter et améliorer la performance du forecasting, tout en reliant directement les erreurs de prévision aux décisions Supply Chain et financières.  
Elle inclut également les méthodes de gestion des risques, du probabilistic forecasting et des événements extrêmes (Black Swans) qui affectent les 18 pays de NOVAFOOD GLOBAL.

---

# 🎯 Objectifs de la section

À la fin de cette section, vous serez capable de :

- Calculer et interpréter les métriques d’accuracy (MAPE, Bias, RMSE, sMAPE)  
- Mesurer la contribution réelle des étapes du processus grâce au FVA (Forecast Value Added)  
- Comprendre l’impact de l’agrégation sur la forecastability  
- Diagnostiquer la prévisibilité d’un SKU via un scoring précis  
- Construire un stock de sécurité robuste basé sur la variabilité  
- Développer des prévisions probabilistes pour anticiper les risques  
- Simuler des crises (Black Swans) et adapter la stratégie S&OP multi-pays  
- Relier précision du forecast → service client → BFR → marge

---

# 🧩 1. Forecast Accuracy — mesurer pour progresser

NOVAFOOD utilise 6 métriques clés de performance :

### 1.1 Forecast Error (FE)

FE = Actual – Forecast


### 1.2 MAPE (Mean Absolute Percentage Error)
Indispensable mais instable sur faible volume.

### 1.3 sMAPE
Plus stable, recommandé pour séries volatiles.

### 1.4 RMSE (Root Mean Square Error)
Très sensible aux gros écarts → utile pour S&OP.

### 1.5 BIAS

BIAS = Sum(Forecast - Actual)

Indique si l’entreprise **sur-prévoit** ou **sous-prévoit** systématiquement.

### 1.6 Forecast Value Added (FVA)
Mesure l’impact des intervenants :
- Sales  
- Marketing  
- Finance  
- DP  
- Modèle statistique baseline  

Objectif :  
➡️ Éliminer les étapes qui dégradent la prévision.

---

# 🧩 2. Impact de l’Agrégation & Forecastability

### 2.1 Pourquoi l’agrégation améliore l’accuracy ?
- Effet loi des grands nombres  
- Compensation des erreurs  
- Réduction du bruit  

NOVAFOOD agrège par :
- Pays  
- Canal  
- Marque  
- Famille produit  
- SKU segmenté ABC/XYZ  

### 2.2 Forecastability Scoring

Score basé sur :
- Coefficient de variation (CV)  
- Intermittence (P0)  
- Volatilité promo  
- Saison forte vs saison faible  
- Historique disponible  

Exemple de score NOVAFOOD :

| Score | Interprétation | Modèle recommandé |
|-------|----------------|-------------------|
| A     | Très prévisible | HW, ARIMA, ML     |
| B     | Moyennement     | MA, SES, HW       |
| C     | Volatile        | SES, Croston, SBA |
| D     | Chaotique       | Naïf, TSB, règles |

---

# 🧩 3. Probabilistic Forecasting — anticiper la variabilité

Dans un monde instable, NOVAFOOD passe progressivement du forecast **deterministic** au forecast **probabilistic**, pour anticiper :

- risques de rupture  
- surstocks  
- pics saisonniers  
- à-temps de production  

### Méthodes utilisées
- Quantile Regression Forest  
- Distribution empirique (bootstrapping)  
- Simulation Monte Carlo  
- Intervalles P90 / P50 / P10  

### Exemple :
Forecast P90 = bon pour stock de sécurité  
Forecast P50 = baseline S&OP  
Forecast P10 = worst case

---

# 🧩 4. Stock de Sécurité & Inventory Management

Le stock de sécurité dépend directement :
- de l’erreur de prévision  
- de la variabilité  
- du service level  
- du lead time  
- du canal  

### Formule classique (service cycle) :

SS = Z * σ_forecast * √LeadTime


### Points clés NOVAFOOD :
- Retail EU → Z = 1.64 (95 %)  
- E-commerce Brésil → Z = 2.05 (97.5 %)  
- Food Service Afrique → Z = 1.28 (90 %)  

### Obsolescence
Pilotée par :
- Fin de vie produit  
- Promotions forcées  
- Migration vers nouvelles gammes

---

# 🧩 5. Risk Management & Black Swans

NOVAFOOD a fait face à plusieurs événements extrêmes :

### Exemples réels :
- Sécheresse Brésil : -22% matières premières  
- Grève portuaire UE : +14 jours de lead time  
- Inondations Vietnam : arrêt de production  
- Inflation Maroc : volatilité prix exceptionnelle  
- Ruptures de transport Kenya → Malaisie

### Outils de gestion :
- Simulation P50/P90  
- Scénarios supply : rerouting, re-priorisation  
- Demand Sensing H+24  
- Capacity smoothing  
- Working capital shield  

---

# 🧪 CAS PRATIQUES NOVAFOOD

---

## **5.1 : MAPE & FVA pour 10 000 SKU multi-pays**
🎯 Objectif :  
Calculer l’accuracy complète d’un portefeuille global NOVAFOOD.

Livrables :  
- Mesures DAX  
- Tableau résultats  
- FVA : Sales, Marketing, Finance, DP

---

## **5.2 : Simulation crise logistique Europe**
🎯 Objectif :  
Simuler un blocage portuaire pendant 4 semaines.

Livrables :
- Tableau impact OTIF  
- Ajustement forecast  
- Décisions S&OP recommandées

---

## **5.3 : Recalibrage stock de sécurité USA**
🎯 Objectif :  
Adapter les stocks de sécurité pour FreshBite USA (volatilité promo).

Livrables :
- Calcul complet SS  
- Variation BFR  
- Impact sur risque de rupture

---

## **5.4 : Probabilistic Forecast FreshBite France**
🎯 Objectif :  
Construire une prévision probabiliste (P10/P50/P90) sur 18 mois.

Livrables :
- Notebook Python  
- Intervalles d’incertitude  
- Risques associés

---

# 📌 Navigation

- [Section 6 — Process, Lean Six Sigma & Systems](../06_Process_Lean_Systems/index.md)  
- [Retour au sommaire FORECASTLAB](../../README.md)

---
