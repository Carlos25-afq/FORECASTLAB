# 07 — Demand Sensing & Real-Time Forecasting  
NOVAFOOD GLOBAL — Prévision Court Terme, POS, Météo & Modèles Adaptatifs

Le Demand Sensing représente la nouvelle frontière du Demand Planning.  
Il permet d’ajuster la prévision **au jour le jour** grâce à l’intégration de signaux externes : données POS, météo, e-commerce temps réel, réseaux sociaux, ruptures transport…  

Chez NOVAFOOD GLOBAL, le Demand Sensing est utilisé pour les gammes sensibles au court terme : **EcoPure**, **FreshBite**, et toutes les références E-commerce.

---

# 🎯 Objectifs de la section

À la fin de cette section, vous serez capable de :

- Comprendre la différence entre forecast traditionnel et demand sensing  
- Construire une prévision court terme basée sur les POS  
- Utiliser la météo comme variable exogène (temp, humidité, pluie, vagues de chaleur)  
- Développer des modèles adaptatifs réajustés toutes les 12h ou 24h  
- Détecter les ruptures de tendance en quasi temps réel  
- Construire une fenêtre glissante 24/48/72 heures E-commerce  
- Mettre en place un pipeline automatique Demand Sensing  
- Intégrer les signaux dans le S&OP et les APS  

---

# 🧩 1. Demand Sensing : qu’est-ce que c’est ?

### Forecast traditionnel = horizon long (1 à 18 mois)  
Basé sur :  
- Historique  
- Tendances  
- Saison  
- Modèles stables

### Demand Sensing = horizon court (24h → 14 jours)  
Basé sur :  
- POS quotidiens  
- Météo  
- Promos en cours  
- Stock en rayon  
- Comportement e-commerce  
- Alerts logistiques temps réel

➡️ Le but : **réduire les erreurs à court terme**, là où l’impact cliente / rupture / surstock est maximal.

---

# 🧩 2. Les signaux utilisés par NOVAFOOD

### **2.1 POS Retail (magasins)**
Variables :
- ventes réelles quotidiennes  
- out-of-stock  
- taux de distribution  
- “store execution” (présence en rayon)  

### **2.2 E-commerce**
Variables :
- clics  
- vues produit  
- taux de conversion  
- ruptures / délais livraison  
- panier moyen  

### **2.3 Météo**
Variables météo les plus corrélées :
- température  
- humidité  
- précipitations  
- vagues de chaleur  
- indice UV  
- météo ressentie  

### **2.4 Logistique & Supply**
- retards transport  
- lead time actualisé  
- congestion portuaire  
- ruptures MP  

---

# 🧩 3. Modèles adaptatifs H+12 / H+24

### Pourquoi ?
Parce que :
- le court terme est dominé par le bruit  
- la demande peut changer rapidement  
- les promotions génèrent des pics instantanés  

### Modèles NOVAFOOD :
1. **ETS adaptatif**  
2. **Prophet + signaux exogènes**  
3. **Linear regression (POS + météo)**  
4. **XGBoost à fenêtre glissante**  
5. **Quantile Regression (distribution)**  

Recalibration toutes les :
- 12 heures (France, Belgique)  
- 24 heures (Brésil, Vietnam)  

---

# 🧩 4. Prévision glissante E-commerce (24h, 48h, 72h)

Le E-commerce est le canal le plus volatile.  
Pour FreshBite Online Brésil, les prévisions se font en **rolling window** :

### Pipeline :
1. Collecte données 48 dernières heures  
2. Feature engineering → météo + comportement utilisateur  
3. Modèle adapté (RF, XGB)  
4. Prévision 24/48/72h  
5. Contrôle qualité  
6. Upload dans SAP IBP

Objectifs :
- réduire ruptures  
- ajuster prix dynamiquement  
- piloter stock web

---

# 🧩 5. Détection de rupture & changement de régime

Outils utilisés :
- CUSUM  
- Moving Z-score  
- Change point detection  
- Prophet changepoints  
- LSTM court-terme (cas e-commerce)

Utilisé sur :
- ruptures météo (canicule → +35%)  
- ruptures logistiques (port UE bloqué)  
- campagnes marketing soudaines  

---

# 🧩 6. Pipeline Demand Sensing NOVAFOOD

Pipeline standardisé global :

RAW POS & Weather → Power Query → Python Model → Forecast CSV → API → SAP IBP


### Étapes :
1. **Power Query** → ingestion POS/météo  
2. **Python** → modèle adaptatif  
3. **Power BI** → visualisation court terme  
4. **API** → envoi APS  
5. **SAP IBP** → recalcul ATP / stock  
6. **S&OE (Execution)** → corrections journalières  

---

# 🧪 CAS PRATIQUES NOVAFOOD

---

## **7.1 : Demand Sensing EcoPure France (POS + météo)**  
🎯 Objectif :  
Créer un modèle court terme intégrant POS + température + précipitations.

Livrables :
- Notebook Python  
- Feature importance  
- Prévision 7 jours  
- Analyse résidus

---

## **7.2 : Prévision glissante 72h E-commerce Brésil**
🎯 Objectif :  
Construire un modèle sliding window 24/48/72h.

Livrables :
- Notebook Python  
- Dashboard Power BI temps réel  
- Upload SAP IBP simulé

---

# 📌 Navigation

- [Section 8 — Ethics & Responsible AI in Forecasting](../08_Ethics_AI/index.md)  
- [Retour au sommaire FORECASTLAB](../../README.md)

---
