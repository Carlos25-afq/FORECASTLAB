# Cas 5.3 — Recalibrage du Stock de Sécurité USA (Probabilistic Safety Stock Modeling)  
NOVAFOOD GLOBAL — Analyse avancée service, coûts & risque

---

## 1. Résumé du cas

NOVAFOOD USA rencontre en 2027 une forte volatilité sur la gamme **FreshBite** :

- croissance commerciale à deux chiffres,
- ruptures fréquentes en E-commerce,
- erreurs de forecast importantes lors des pics de demande,
- complexité logistique importante (réseau étendu, plusieurs entrepôts).

La Direction Supply Chain USA demande un **recalibrage complet du stock de sécurité**, mais veut éviter un simple calcul “classique” basé sur :
\[
SS = z \times \sigma \times \sqrt{LT}
\]

Elle veut désormais une approche **probabiliste**, basée sur :

- la distribution des erreurs de prévision,
- des quantiles,
- une simulation Monte Carlo,
- trois niveaux de service alternatifs :
  - 92%
  - 96%
  - 98.5%

Vous êtes le **Demand Planner Senior USA**, en charge de :

- analyser l’historique d’erreurs de prévision,
- déterminer une distribution réaliste,
- modéliser la demande future probabiliste,
- recalibrer les stocks de sécurité,
- recommander le meilleur compromis coût/service.

---

## 2. Compétences visées

- Modélisation de l’incertitude du forecast  
- Analyse de distributions (normal, skewed, heavy-tailed)  
- Calcul de safety stock par quantile  
- Simulation Monte Carlo  
- Sélection niveau de service optimal  
- Présentation d'un business case complet au VP Supply Chain USA  

---

## 3. Dataset

📂 Dataset attendu :  
`datasets/novfood_case_studies/S5_3_SafetyStock_USA.csv`


---

## 4. Travail demandé — Étapes détaillées

---

### 🔹 **Étape 1 — Analyser la distribution d’erreurs**

À partir des données `Forecast_Error_History` :

1. Construire l’histogramme  
2. Identifier la forme :  
   - normal ?  
   - skewed ?  
   - heavy-tailed (fat tails) ?  
3. Tester le fit statistique (KS test ou visuel si Excel)

📌 *Question 1 : Décrivez la nature de la distribution (skewed, kurtosis, outliers).*

---

### 🔹 **Étape 2 — Safety stock basé sur quantile**

Si on note \( Q_p \) le quantile p du forecast error :

\[
SS_p = Q_p \times \sqrt{LT}
\]

Calculer le SS pour :

- 92% → quantile Q0.92  
- 96% → quantile Q0.96  
- 98.5% → quantile Q0.985  

📌 *Question 2 : Quel niveau de SS correspond à chaque quantile ?*

---

### 🔹 **Étape 3 — Simulation Monte Carlo**

Simuler **10 000 itérations** pour générer des scénarios de demande future :

- échantillonnage aléatoire dans la distribution d’erreurs,
- ajout au forecast moyen,
- calcul des excès de demande.

Sorties attendues :

- histogramme des ruptures,
- probabilité d’atteindre le niveau de service cible,
- estimation du stock nécessaire pour 95% de stabilité.

📌 *Question 3 : Quel est le SS optimal obtenu par simulation ?*

---

### 🔹 **Étape 4 — Coût total (Total Cost Minimization)**

Pour chaque niveau de stock de sécurité SS_p :

Coût total =  
\[
TC = SS_p \times Unit\_Cost + (Ruptures_p \times Stockout\_Penalty\_Cost)
\]

Ruptures_p estimées via Monte Carlo.

📌 *Question 4 : Quel SS minimise le coût total ?*

---

### 🔹 **Étape 5 — Analyse portefeuille (100 SKU)**

- Appliquer la méthode à 100 SKU USA.  
- Classer les SKU en 3 catégories :
  - sous-stockés  
  - équilibrés  
  - sur-stockés  

📌 *Question 5 : Combien de SKU nécessitent un recalibrage urgent ?*

---

### 🔹 **Étape 6 — Recommandation finale**

Synthèse à fournir au VP Supply Chain USA :

- niveau optimal de service recommandé (92 / 96 / 98.5)  
- coût total projeté  
- gains potentiels sur :
  - ruptures  
  - cash immobilisé  
  - service client  
- actions à lancer :
  - ajustement des SLA  
  - communication Sales/Finance  
  - recalibrage trimestriel  
  - intégration du forecast probabiliste dans S&OP

📌 *Question 6 : Rédigez la recommandation (12–15 lignes max).*

---

## 5. Livrables attendus

- Notebook Python ou Excel Monte Carlo  
- Calculs SS multi-quantiles  
- Tableau service/cost par niveau  
- Clustering sous-stocké / sur-stocké  
- Recommandation finale  

---

## 6. Critères d’évaluation

- Correctitude statistique (quantiles cohérents)
- Qualité du Monte Carlo  
- Clarté des hypothèses  
- Choix de stratégie justifié  
- Recommandation crédible business  

---

## 7. Extensions (niveau expert)

- Safety stock dynamique selon horizon (H1, H2, H3)  
- Modèle Bayesian update  
- Séries en non-normalité marquée (t-Student, Cauchy)  
- Simulation multi-entrepôts (réseau USA)  

---
