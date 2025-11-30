# 03 — Core Time Series Forecasting  
NOVAFOOD GLOBAL — Modèles de Prévision Basés sur l’Historique

Cette section constitue le cœur statistique du métier : les modèles de séries temporelles.  
Elle introduit les principes fondamentaux du forecasting, les limites réelles rencontrées en entreprise, les méthodes classiques et avancées utilisées pour les 32 000 SKU de NOVAFOOD GLOBAL, ainsi que les pièges statistiques auxquels tout Demand Planner doit rester vigilant.

---

# 🎯 Objectifs de la section

À l’issue de cette section, vous serez capable de :

- Comprendre les **6 grands mythes du forecasting**  
- Analyser et reconnaître les motifs récurrents des séries temporelles NOVAFOOD  
- Appliquer les modèles simples (Naïf, MA, SES) et leurs variantes  
- Construire un modèle Holt-Winters complet (additif / multiplicatif)  
- Paramétrer et diagnostiquer ARIMA / SARIMA  
- Modéliser les demandes intermittentes via **Croston / SBA / TSB**  
- Combiner plusieurs modèles en portfolio multi-pays  

---

# 🧩 1. Les 6 mythes du forecasting (version NOVAFOOD)

Les prévisionnistes débutants tombent souvent dans ces pièges.  
Voici comment NOVAFOOD les traite.

### **Mythe 1 — “On peut prédire le futur”**
Faux.  
On peut *estimer* le signal, jamais éliminer le bruit.  
Le rôle du DP est d'évaluer l’incertitude, pas de produire des valeurs parfaites.

### **Mythe 2 — “Il existe un modèle miracle”**
Aucun modèle n’est stable sur 18 pays.  
Chaque SKU a son propre régime :  
- saisonnalité claire  
- non-stationnarité  
- rupture de tendance  
- promotions  
- climat  
- comportement chaotique e-commerce

### **Mythe 3 — “Un bon fit = un bon forecast”**
Un modèle peut coller parfaitement au passé… et échouer sur le futur.

→ Overfitting = ennemi #1 du Demand Planner.

### **Mythe 4 — “Les modèles sophistiqués sont les meilleurs”**
Chez NOVAFOOD, 72% du portfolio fonctionne mieux avec :  
➡️ SES / Holt simple / MA / WMA  
Seulement 9% nécessite ARIMA / ML.

### **Mythe 5 — “L’IA peut tout prédire”**
Non.  
Les algorithmes apprennent le *passé*.  
Ils échouent lors de ruptures : grève portuaire, sécheresse Brésil, taxe export Vietnam…

### **Mythe 6 — “Plus de données = meilleure prévision”**
Plus de données = plus de bruit.  
Le secret : *nettoyage, segmentation, sélection de features*.

---

# 🧩 2. Méthodes simples : baseline des prévisions NOVAFOOD

Ces modèles sont utilisés pour 40–60% des SKU.

### **2.1 Modèle Naïf**
Forecast(t) = Actual(t-1)  
Très robuste ⇒ baseline interne NOVAFOOD.

### **2.2 Moving Average (MA)**
Lisse la volatilité.  
- MA(3), MA(6), MA(12)  
- Utilisé pour les séries “douces”.

### **2.3 Weighted Moving Average (WMA)**
Plus de poids sur les derniers mois.

### **2.4 Simple Exponential Smoothing (SES)**
Forecast(t) = α × Actual(t-1) + (1-α) × Forecast(t-1)

α = 0,1 → lissage fort  
α = 0,5 → réactivité accrue

---

# 🧩 3. Holt-Winters : tendance + saisonnalité

Modèles utilisés pour :  
- NutriBox EU (saison plateau hiver/été)  
- EcoPure Asia (saisonnalité logistique)  
- FreshBite US (effet promotions régulières)

### Holt
- Niveau  
- Tendance  

### Holt-Winters
- Additif : variations constantes  
- Multiplicatif : variations proportionnelles  

### Processus :
1. Initialisation  
2. Mise à jour des composantes  
3. Forecast n périodes  
4. Re-saisonnalisation

---

# 🧩 4. Décomposition saisonnière

Utilisée lors de la phase “Analyse” du S&OP.

### Étapes :
1. Centrage (moving average)  
2. Extraction du trend  
3. Extraction de la saisonnalité  
4. Résidus  
5. Reconstruction

Permet de **comprendre** avant de **prédire**.

---

# 🧩 5. ARIMA / SARIMA — Modèles avancés

Utiles sur 8 à 12% des séries NOVAFOOD.

### 5.1 Composantes :
- **AR** (Auto-Regressive)  
- **I** (Integrated : différenciation)  
- **MA** (Moving Average)  
- **SARIMA** pour la saisonnalité forte  

### 5.2 Diagnostics :
- ACF / PACF  
- Tests Dickey-Fuller  
- Analyse des résidus (Ljung-Box)

### 5.3 Limites :
- Fragiles aux ruptures  
- Demande un historique propre  
- Overfitting fréquent  
- Maintenance trimestrielle nécessaire

---

# 🧩 6. Demandes intermittentes : Croston / SBA / TSB

NOVAFOOD gère 11 200 SKU E-commerce avec demande intermittente.

### 6.1 Croston
Sépare :  
- la taille des ventes  
- l’intervalle entre ventes

### 6.2 SBA (Syntetos–Boylan)
Réduction du biais.

### 6.3 TSB
Ajoute probabilité de demande à chaque pas.

---

# 🧪 CAS PRATIQUES NOVAFOOD

---

## **3.1 : Prévision NutriBox France sur 36 mois**  
🎯 Objectif :  
Construire un modèle Holt-Winters multiplicatif complet.

Livrables :  
- Excel + initialisation complète  
- Graphiques trend / saison / résidus  
- Forecast 12 mois

---

## **3.2 : Prévision EcoPure Vietnam (ARIMA)**  
🎯 Objectif :  
Identifier (p,d,q) avec ACF/PACF + construction sous Python.

Livrables :  
- Notebook Python  
- Tableau diagnostics  
- Résidus commentés

---

## **3.3 : Demande intermittente E-commerce Afrique (Croston / SBA / TSB)**  
🎯 Objectif :  
Comparer les 3 modèles sur SKU longue traîne.

Livrables :  
- Notebook Python  
- Courbes forecast vs actual  
- Analyse erreurs (MAE, MASE, Bias)

---

## **3.4 : Prévision combinée multi-pays NutriBox**  
🎯 Objectif :  
Construire une prévision combinée :  
→ France + Espagne + Italie + Belgique

Livrables :  
- Excel + DAX  
- Modèle d’agrégation  
- Recommandations S&OP

---

# 📌 Navigation

- [Section 4 — Advanced Models : Causal, ML, NPD, Promotions](../04_Advanced_Models/index.md)  
- [Retour au sommaire FORECASTLAB](../../README.md)

---
