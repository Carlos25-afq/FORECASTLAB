# Cas 5.2 — Simulation d’une crise logistique Europe  
Impact sur service, stocks et prévisions — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

En 2027, NOVAFOOD GLOBAL fait face à une **crise logistique majeure en Europe** :

- Grèves portuaires en Belgique et aux Pays-Bas,
- Saturation des entrepôts,
- Allongement brutal des lead times de transport de +40 à +80%,
- Capacité limitée des transporteurs routiers.

Les hubs EU (principalement le **hub logistique de Belgique**) alimentent :

- la France,  
- l’Allemagne,  
- l’Espagne,  
- l’Italie,  
- la Scandinavie.

La Direction Supply Chain souhaite comprendre :

1. L’impact de cette crise sur les **niveaux de service**  
2. Les conséquences sur les **stocks de sécurité et les ruptures**  
3. Comment adapter les **paramètres de réapprovisionnement**  
4. Comment ajuster la **prévision opérationnelle** pendant la crise

Vous êtes le **Demand & Supply Planner Europe** chargé de :

- construire une **simulation de crise logistique**,  
- quantifier son impact,  
- proposer des **scénarios d’atténuation** et un plan d’action.

---

## 2. Compétences visées

- Comprendre le lien **Lead time – Stock – Service**  
- Traduire une crise transport en **hypothèses chiffrées**  
- Simuler différents scénarios de lead time et de variabilité  
- Mesurer l’impact sur :
  - le fill rate,  
  - le niveau de stock moyen,  
  - les ruptures.  
- Construire une **recommandation de mitigation** :
  - surstocks ciblés,  
  - priorisation clients/pays,  
  - ajustement forecast court terme.

---

## 3. Contexte NOVAFOOD — Hub Europe

Caractéristiques :

- Hub principal : **Belgique**  
- Usine d’origine : France + Maroc  
- Clients livrés : FR, DE, ES, IT, BE, NL, Nordics  
- Produits : NutriBox, EcoPure, FreshBite, VitalMeal  

Avant crise :

- Lead Time moyen : 7 jours  
- Écart-type (σ_LT) : 1,5 jours  
- Niveau de service cible : 97%  

Pendant crise :

- Lead Time passe à 12–15 jours  
- Variabilité (σ_LT) double  
- Capacité warehouse limitée → pas possible de surstocker tout le portefeuille

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S5_2_Crise_Logistique_Europe.csv`


---

## 5. Travail demandé — Étapes détaillées

---

### Étape 1 — Rappel théorique : Stock de sécurité

Rappels de base :

\[
SS = z \times \sqrt{LT \times \sigma_D^2 + \mu_D^2 \times \sigma_{LT}^2}
\]

où :

- \( SS \) = stock de sécurité  
- \( z \) = facteur de service (ex : z = 1,88 pour 97%)  
- \( LT \) = lead time  
- \( \sigma_D \) = écart-type de la demande journalière  
- \( \sigma_{LT} \) = écart-type du lead time  

📌 **Question 1 :**  
Expliquez qualitativement ce qu’il se passe si on augmente LT et σ_LT.

---

### Étape 2 — Calcul stock de sécurité avant/après crise

Pour un échantillon de **SKU critiques (Top 500)** :

1. Calculer SS avant crise.  
2. Calculer SS pendant crise (LT et σ_LT augmentés).  
3. Calculer la **variation %** du stock de sécurité.

📌 **Question 2 :**  
De combien augmente le stock de sécurité requis, en moyenne, sur ces SKU ?

---

### Étape 3 — Impact sur service si le SS n’est pas ajusté

Hypothèse :

- On ne change **pas** les stocks de sécurité (contraintes de cash / place)
- On laisse le SS “pré-crise”

Calculer le **nouveau niveau de service effectif** avec LT augmenté.

📌 **Question 3 :**  
Quel est le nouveau niveau de service moyen ?  
Certaines gammes descendent-elles sous 90% ?

---

### Étape 4 — Simulation de scénarios de mitigation

Construire au moins 3 scénarios :

#### 🔹 Scénario A — “Survival mode”
- On augmente le SS **uniquement** sur les 20% de SKU les plus stratégiques (A / VitalMeal hôpitaux, grandes enseignes clés, etc.)
- Les autres restent à SS pré-crise

#### 🔹 Scénario B — “Balanced”
- On augmente modérément les SS sur 50% du portefeuille
- On priorise les SKU à forte marge et grosse rotation

#### 🔹 Scénario C — “Full protection”
- On ajuste le SS pour conserver 97% de service sur tout le portefeuille
- Coût stock + coût cash maximal

Pour chaque scénario, estimer :

- Niveau de service moyen  
- Service par gamme / pays  
- Coût supplémentaire de stock  
- Coût des ruptures (si service < cible)  

📌 **Question 4 :**  
Quel scénario offre le meilleur compromis **service + coût** ?

---

### Étape 5 — Lien avec la prévision (forecast)

Pendant la crise :

- L’incertitude opérationnelle augmente  
- Certains pays veulent augmenter fortement leurs commandes “par peur”  
- Le risque de “bullwhip effect” est élevé

Travail demandé :

- Proposer des **règles d’ajustement forecast** court terme :
  - limiter les sur-ajustements Sales “défensifs”,  
  - utiliser un **range forecasting** (min/base/max),  
  - intégrer les contraintes de capacité logistique dans le consensus.

📌 **Question 5 :**  
Rédigez 5 règles concrètes pour adapter le process de prévision pendant une crise logistique.

---

### Étape 6 — Recommandation finale à la Direction Europe

Synthèse écrite à fournir :

- Impact chiffré de la crise sur :
  - service,  
  - stock,  
  - cash,  
  - risque de ruptures.  
- Choix de scénario (A, B ou C)  
- Proposition d’actions :
  - priorisation clients / pays,  
  - gel de certaines promotions,  
  - ajustement des SLA pour certains clients,  
  - communication clients.

📌 **Question 6 :**  
Rédigez une note (10–12 lignes) à la Direction Supply Chain Europe présentant vos recommandations.

---

## 6. Livrables attendus

- Fichier Excel ou notebook Python avec :
  - calculs SS avant/après crise,  
  - niveaux de service simulés,  
  - comparaison des scénarios A/B/C.  
- Tableau de synthèse :
  - Service, Stock, Coût, Risque par scénario.  
- Note de recommandation (1 page max).

---

## 7. Critères d’évaluation

- Compréhension claire du lien LT–SS–Service  
- Qualité des simulations (formules correctes, hypothèses explicites)  
- Pertinence de la segmentation des SKU  
- Réalisme des scénarios de mitigation  
- Clarté de la recommandation finale

---

## 8. Extensions (niveau expert)

- Simulation Monte Carlo des lead times (distribution empirique)  
- Forecast probabiliste couplé à SS dynamique  
- Intégration de contraintes transport (capacité, coût)  
- Optimisation multi-objectifs : minimiser coût total (stock + rupture + transport)  
- Modélisation sur horizon 6–12 mois avec normalisation post-crise

---
