# 04 — Advanced Models  
NOVAFOOD GLOBAL — Causal Models, Machine Learning, Promotions & New Products

Après la maîtrise des séries temporelles classiques, le Demand Planner moderne doit comprendre les modèles avancés : causalité, machine learning, uplift promotionnel, cannibalisation produit et prévision des innovations.  
Chez NOVAFOOD GLOBAL, ces modèles sont utilisés pour les segments stratégiques : innovations FreshBite, pricing NutriBox, promotions VitalMeal et élasticités multi-pays.

---

# 🎯 Objectifs de la section

À la fin de cette section, vous serez capable de :

- Construire des modèles causaux robustes (prix, promo, météo, distribution)  
- Déterminer les élasticités clés dans un marché FMCG  
- Modéliser un uplift promotionnel avec ML  
- Identifier et mesurer la cannibalisation entre produits  
- Construire un modèle NPD complet (Looks-like, S-curve, Markov)  
- Mettre en œuvre du Machine Learning explicable sur les prévisions  
- Créer un portefeuille de modèles adaptés aux types de SKU NOVAFOOD

---

# 🧩 1. Causal Models — comprendre les “drivers” de la demande

Les modèles causaux permettent d’expliquer *pourquoi* la demande évolue.

### Principales variables causales NOVAFOOD
- **Prix** (Price Index, Price Variations, Elasticity)  
- **Promotions** (Discount %, Display, Leaflet)  
- **Distribution** (Numeric Distribution, Weighted Distribution)  
- **Météo** (température, pluie, vagues de chaleur)  
- **Concurrence** (prix concurrents, cannibalisation interne)  
- **Marketing** (campagnes, retours TV, influenceurs)

### Modèle causal simple — exemple NutriBox Maroc

```plaintext
Demand = β0 + β1*Price + β2*Promo + β3*Distribution + β4*Temperature + ε

### KPI causaux indispensables

* Elasticité prix
* Elasticité promo
* Incremental Sales
* Baseline vs Incremental Split

### 🧩 2. Promotional Uplift Models (Promo Forecasting)

Indispensable pour NOVAFOOD Brésil et Europe où le calendrier promotionnel structure les ventes.

**Types de promotions**

* Réduction prix
* Bundles
* “Buy 2 Get 1”
* Display magasin
* Catalogue distributeur

**Méthodes**

* Modèles additifs (baseline + uplift)
* Regression with dummy variables
* Prophet + regressors
* Machine Learning (Random Forest, XGBoost)
* Uplift Modeling (treatment vs control)

**Livrables S&OP**

* Incremental Volume
* Incremental Margin
* Expected ROI Promotionnel
* Impact sur capacité usine

### 🧩 3. Cannibalisation — impact produit vs produit

NOVAFOOD gère plusieurs familles cannibales :

* FreshBite Classic, FreshBite Zero, FreshBite Vegan.

**Approches de mesure :**

* Modèle multi-régression
* Modèle part de marché
* Cross-price elasticity
* Modèle Markov de transition (pré et post lancements)

**Exemple :**
Si FreshBite Zero cannibalise 18 % de FreshBite Classic →
→ Ajustement forecast baseline
→ Ajustement production / stock
→ Ajustement pricing

### 🧩 4. Machine Learning — Forecasting augmenté

NOVAFOOD utilise le ML sur les segments :

* E-commerce haute volatilité
* Promotions complexes
* Segmentation par forecastability
* Breakdowns multi-pays (Asie / LatAm)

**Modèles principaux**

* Decision Trees
* Random Forest
* Gradient Boosting (XGBoost)
* CatBoost
* Prophet (avec exogenous regressors)

**Pipeline ML type**

* Feature engineering
* Segmentation du dataset
* Feature selection
* Training / validation
* Explainability (SHAP)
* Deployment (Power BI, Python API)

### 🧩 5. New Product Forecasting (NPD)

Les innovations NOVAFOOD suivent 4 étapes analytiques :

**5.1 Looks-Like Analysis**
Trouver un produit analogue comparable.
Ex. FreshBite Vegan ← FreshBite Classic (ajusté).

**5.2 Diffusion S-Curve**
Application du modèle Bass ou Gompertz.

**5.3 Analogous Forecast**
Courbe d’adoption basée sur un produit similaire.

**5.4 Markov Process — transition de parts de marché**
Utilisé pour les gammes FreshBite post-lancement.

**Exemple matrice de transition :**

| From / To | Classic | Zero | Vegan |
| :---: | :---: | :---: | :---: |
| Classic | 0.80 | 0.12 | 0.08 |
| Zero | 0.15 | 0.70 | 0.15 |
| Vegan | 0.10 | 0.08 | 0.82 |

### 🧪 CAS PRATIQUES NOVAFOOD

**4.1 : Élasticité prix NutriBox Maroc**

* 🎯 **Objectif :**
    Construire un modèle causal complet pour estimer l’élasticité prix sur 3 ans.
* **Livrables :**
    Dataset multi-variates
    Régression Excel + Python
    Interprétation business (Sales & Finance)

**4.2 : Modèle promotionnel VitalMeal Brésil**

* 🎯 **Objectif :**
    Mesurer l’uplift de promotions fortes sur 52 semaines.
* **Livrables :**
    Modèle causal + ML
    Uplift estimation
    Impact sur capacité usine

**4.3 : Lancement FreshBite Vegan — Forecasting NPD complet**

* 🎯 **Objectif :**
    Construire un modèle Looks-Like + diffusion + Markov.
* **Livrables :**
    Notebook Python
    Courbes d’adoption
    Recommandations marché

**4.4 : Cannibalisation FreshBite Classic vs Zero**

* 🎯 **Objectif :**
    Mesurer et corriger le cross-demand effect entre gammes.
* **Livrables :**
    Analyse cross-price elasticity
    Courbe ajustée baseline
    Impact S&OP

### 📌 Navigation

* [Section 5 — Performance, Forecastability, Inventory & Risks]
* [Retour au sommaire FORECASTLAB]