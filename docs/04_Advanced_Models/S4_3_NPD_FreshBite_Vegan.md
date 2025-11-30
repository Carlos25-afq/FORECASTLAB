# Cas 4.3 — Lancement FreshBite Vegan : Forecasting NPD complet  
Méthodes Looks-Like, S-Curve, Analogie & Processus de diffusion  
NOVAFOOD GLOBAL — New Product Forecasting Excellence

---

## 1. Résumé du cas

NOVAFOOD GLOBAL lance en 2026 un nouveau produit stratégique :  
**FreshBite Vegan**, une barre nutritionnelle 100% végétale, destinée aux marchés Europe & APAC.

Le lancement est classé comme **innovation incrémentale forte**, avec :

- un nouveau segment consommateur ciblé (vegan, healthy snack),  
- une concurrence déjà installée mais fragmentée,  
- un marché projeté en croissance rapide,  
- une forte incertitude sur les volumes de départ.

Les objectifs du COMEX :

1. **Estimer la demande des 12 premiers mois**,  
2. Fournir une **prévision de lancement robuste**,  
3. Simuler la croissance attendue via **S-curve**,  
4. Construire un modèle d’analogie avec FreshBite Classic & Zero,  
5. Anticiper la **part de marché** via un modèle **Markov**.

Votre rôle, en tant que **Demand Planner Europe FreshBite**, est de concevoir un forecasting NPD complet, prêt à être présenté au S&OP Global.

---

## 2. Compétences visées

### 🔍 Analyse & méthodologie NPD
- Comprendre le cycle de lancement (NPD gate process)  
- Collecter les inputs de Marketing & Insights  
- Structurer les hypothèses de lancement

### 📈 Méthodes de prévision NPD
- **Looks-Like Analysis** (analogie interne)  
- **Analogie externe** (marchés comparables)  
- **Bass/S-Curve Diffusion Model**  
- **Markov Transition Model** (long-run market share)

### 🔮 Scénarios & incertitude
- Prévoir avec faible historique  
- Scénarios High / Base / Low  
- Analyse de sensibilité  

### 🧠 Communication S&OP
- Argumenter des hypothèses  
- Communiquer la prévision avec clarté et transparence  
- Intégrer risques & opportunités

---

## 3. Contexte NOVAFOOD — FreshBite Vegan

Les marchés concernés :

- France 🇫🇷  
- Belgique 🇧🇪  
- Allemagne 🇩🇪  
- Vietnam 🇻🇳  
- Malaisie 🇲🇾  

Concurrence : VegaBar, NutriGreen, HerbalLife Snack.

Données internes disponibles :

- Historique 36 mois FreshBite Classic  
- Historique 24 mois FreshBite Zero  
- Ventes initiales des concurrents sur 12–18 mois  
- Études marketing sur adoption vegan  

---

## 4. Jeu de données

📂 Cible :  
`datasets/novfood_case_studies/S4_3_FreshBite_Vegan_NPD.csv`

 

---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Analyse du contexte NPD

1. Identifier les drivers de succès  
2. Évaluer la base consommateur  
3. Définir 3 scénarios :  
   - **Base**  
   - **Optimiste**  
   - **Pessimiste**

📌 **Question 1 :**  
Quels sont les 5 risques clés du lancement FreshBite Vegan ?

---

### Étape 2 — Looks-Like Analysis interne

Comparer FreshBite Vegan à :

- FreshBite Classic  
- FreshBite Zero  

Calculer :

- ratio de conversion (ex : Vegan = 0.45 × Classic)  
- vitesse d’adoption initiale  
- ramp-up (vitesse de montée)

📌 **Question 2 :**  
Quel SKU sert d’analogue principal ? Pourquoi ?

---

### Étape 3 — Analogie externe

Construire une prévision basée sur :

- produits concurrents (VegaBar, NutriGreen),  
- données APAC,  
- progression de marché vegan.

📌 **Question 3 :**  
Quelle différence clé existe-t-il entre analogue interne et externe ?

---

### Étape 4 — Modèle S-Curve (diffusion Bass)

Utiliser une S-curve :

\[
Adoption(t) = \frac{M}{1 + e^{-k(t-t_0)}}
\]

Ou modèle Bass :

\[
S(t) = p(M - Y_{t-1}) + q\frac{Y_{t-1}}{M}
\]

où :

- **p** = coefficient d'innovation  
- **q** = coefficient d'imitation  
- **M** = marché maximum  

Créer :

- courbe d’adoption  
- forecast 12 mois  
- analyse early adopters vs imitators

📌 **Question 4 :**  
Le marché FreshBite Vegan semble-t-il "innovation-driven" ou "imitation-driven" ?

---

### Étape 5 — Modèle Markov pour part de marché

Définir :

- États : FreshBite Vegan, Classic, Zero, Concurrence  
- Matrice de transition 4×4  
- Estimer :
  - parts de marché à 3 mois  
  - long-run market share (limite de Markov)

📌 **Question 5 :**  
Après convergence, quelle part de marché FreshBite Vegan atteint-elle ?

---

### Étape 6 — Construction du Forecast NPD final

Fusionner :

- Looks-Like  
- S-curve  
- Markov  
- Scénarios high/base/low

Livrer :

- 3 trajectoires 12 mois  
- narrative (risques + opportunités)  
- recommandation de recettes / volumes de lancement

📌 **Question 6 :**  
Rédigez une narration S&OP Europe (10 lignes) pour le lancement FreshBite Vegan.

---

## 6. Livrables attendus

- Notebook Python / Excel complet  
- Modèles Looks-Like, S-curve et Markov  
- Forecast Base / High / Low  
- Présentation S&OP (1 slide)  
- Analyse des hypothèses + justification  

---

## 7. Critères d’évaluation

- Qualité méthodologique  
- Robustesse des analogies  
- Cohérence du forecast  
- Compréhension de la diffusion  
- Clarté S&OP  

---

## 8. Extensions (niveau expert)

- NPD multi-pays : adoption différenciée par pays  
- Modèle conjoint prix + diffusion  
- Optimisation marketing spend pour maximiser l’adoption  
- Approche Bayesian NPD (MCMC)  
- Corrélation NPD × cannibalisation FreshBite Classic  

---
