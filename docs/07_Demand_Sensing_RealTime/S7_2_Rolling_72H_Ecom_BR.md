# Cas 7.2 — Prévision 72h glissante E-commerce Brésil  
Real-Time Forecasting, Machine Learning adaptatif & signaux événementiels  
NOVAFOOD GLOBAL — Gamme FreshBite & EcoPure (Brésil)

---

## 1. Résumé du cas

NOVAFOOD Brésil connaît une explosion des ventes E-commerce (+38% YoY).  
Cependant, ce canal est **extrêmement volatile**, influencé par :

- promotions flash,
- campagnes digitales,
- météo tropicale instable,
- ruptures entrepôt,
- variation du trafic web,
- événements e-commerce (Mega Liquidação, Prime Day Amazon BR),
- délais de livraison fluctuants.

La Direction LATAM demande la création d’un **forecast temps réel 72h glissant**, recalculé :

- toutes les 3 heures,
- intégrant signaux forts et signaux faibles,
- pour optimiser :
  - le picking,
  - le staffing entrepôt,
  - l’allocation du stock,
  - les lead times logistiques,
  - la gestion des ruptures rapides.

Vous êtes le **Demand Sensing Specialist LATAM**, chargé de :

1. Construire un modèle temps réel 72h,  
2. Intégrer POS online (ventes minute / heure),  
3. Ajouter signaux web (trafic, ajout panier),  
4. Intégrer météo tropicale,  
5. Produire un **range forecast** + “alertes risque”.

---

## 2. Compétences visées

- Prévision temps réel E-commerce (minute → heure → jour)  
- Feature engineering haute fréquence  
- ML adaptatif court horizon  
- Détection d’événements e-commerce  
- Construction d’un forecast 72h glissant (H+1 → H+72)  
- Détection anomalies web/ventes  
- Approche risk-based (min/base/max)  
- Recommandation logistique en temps réel  

---

## 3. Dataset

📂 Dataset recommandé :  
`datasets/novfood_case_studies/S7_2_Forecast_72h_Ecommerce_BR.csv`

Variables :

### Ventes & signaux E-commerce
- `Timestamp`
- `Sales_Online`
- `Cart_Additions`
- `Session_Count`
- `Conversion_Rate`
- `Abandon_Rate`
- `Product_Page_Views`
- `Traffic_Source` (Organic / Paid / Email / Social)

### Logistique & stocks
- `Inventory_Warehouse`
- `Shipment_Delay`
- `LeadTime_Hours`
- `Capacity_Constraint_Flag`

### Météo
- `Temperature`
- `Humidity`
- `Rain_Probability`

### Événements
- `Event_Flag` (Prime Day, Mega Sale)
- `Flash_Promo_Flag`

---

## 4. Travail demandé — Étapes détaillées

---

### 🔹 Étape 1 — Analyse haute fréquence (minute / heure)

Objectifs :

- détecter des patterns horaires,  
- analyser l’impact du trafic,  
- identifier les pics événementiels.

Travail :

- moyenne des ventes par heure,  
- courbes trafic web vs ventes,  
- impact d’une pluie tropicale sur les commandes,  
- détection sessions anormales.

📌 **Question 1 : quelle variable haute fréquence explique le mieux les ventes ?**

---

### 🔹 Étape 2 — Construction du modèle 72h glissant

Recommandation : modèle hybride  
- **Short-term ML** (XGBoost / Random Forest courte fenêtre)  
- **Exponential Smoothing** pour stabiliser  
- **Régression multivariée** (trafic, météo, promo)

Forme générale :

\[
Sales_{t+1..t+72} = f(Traffic, Cart, Temp, Events, Lag\ Sales)
\]

📌 **Question 2 : quel modèle donne le meilleur RMSE 72h ?**

---

### 🔹 Étape 3 — Bande d’incertitude (min/base/max)

Construire :

- P10 (min),
- P50 (base),
- P90 (max),

pour chaque horizon H+1, H+3, H+6, H+12, H+24, H+48, H+72.

Outputs attendus :

- fan chart,
- tableau de quantiles,
- probabilité dépassement stock.

📌 **Question 3 : quelle est la probabilité de rupture H+48 ?**

---

### 🔹 Étape 4 — Gestion événementielle

Établir des règles automatiques :

- si `Event_Flag = 1`, augmenter trafic +25%,
- si `Flash_Promo_Flag = 1`, conversion +60%,
- si `Rain_Probability > 0.7`, trafic mobile augmente,
- si `Shipment_Delay > 4h`, chute conversion.

📌 **Question 4 : quel est l’impact d’un Prime Day sur la demande 24h ?**

---

### 🔹 Étape 5 — Détection des anomalies & alertes

Détection :

- ventes anormalement hautes,
- trafic incohérent,
- rupture imminente,
- emballement promo non prévu.

Méthodes possibles :

- isolation forest,
- rolling z-score,
- IQR.

📌 **Question 5 : quels signaux indiquent un risque imminent de rupture ?**

---

### 🔹 Étape 6 — Recommandations opérationnelles temps réel

Inclure :

- réallocation de stock entre entrepôts,  
- accélération expédition,  
- changement SLA,  
- activation transport urgent,  
- réduction des délais picking,  
- alerte automatique équipe warehouse.

📌 **Question 6 : recommandez un plan opérationnel pour les prochaines 48 heures.**

---

## 5. Livrables attendus

- Notebook Python ML temps réel  
- Prévision 72h glissante (H+1→H+72)  
- Graphique fan chart  
- Détection anomalies  
- Algorithme d’alerting  
- Recommandation écrite  

---

## 6. Critères d’évaluation

- Performance prévision 72h  
- Pertinence du feature engineering  
- Qualité des signaux événementiels  
- Détection anomalies cohérente  
- Recommandation opérationnelle réaliste  

---

## 7. Extensions (expert++)

- Pipeline complet API temps réel (Kafka, Kinesis)  
- Dashboard Power BI streaming dataset  
- Prévision 5 minutes glissante  
- Modèle deep learning LSTM court terme  
- Optimisation transport H+3 / H+6  
- Auto-calibration continue  

---
