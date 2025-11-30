# Cas 3.2 — Prévision EcoPure Vietnam avec ARIMA / SARIMA  
NOVAFOOD GLOBAL — Analyse de stationnarité, différenciation et sélection de modèle

---

## 1. Résumé du cas

EcoPure est la gamme “boisson santé naturelle” de NOVAFOOD.  
Le marché vietnamien est extrêmement dynamique, fortement impacté par :

- la saison des pluies et des chaleurs extrêmes,
- des promotions massives en retail,
- une concurrence agressive des boissons locales.

La demande EcoPure Vietnam est **irrégulière**, avec des sauts de niveau structurels.  
Ce cas te met dans la peau du **Demand Planner Vietnam**, chargé de modéliser la série sur 48 mois pour produire un forecast robuste.

---

## 2. Compétences visées

- Comprendre et détecter la **non-stationnarité**
- Utiliser les tests ADF / KPSS
- Lire et interpréter **ACF / PACF**
- Utiliser Python pour modéliser ARIMA / SARIMA
- Sélectionner les paramètres (p, d, q) et (P, D, Q)
- Validation du modèle via :
  - résidus,
  - Ljung-Box test,
  - comparaison AIC/BIC
- Construire une **narration business Vietnam** compréhensible pour S&OP

---

## 3. Contexte NOVAFOOD — EcoPure Vietnam

- Marque : **EcoPure**
- Pays : **Vietnam**
- Horizon : **48 mois (4 ans)**
- Granularité : **mensuelle**
- Canal : Retail uniquement
- Variables explicatives externes possibles :
  - Température moyenne,
  - Niveau de précipitations,
  - Indicateur de promotion mensuelle.

L’objectif n’est pas encore d’utiliser les variables exogènes (ce sera en section 4),  
mais de **trouver un modèle ARIMA / SARIMA performant sur la série non transformée**.

---

## 4. Jeu de données

📂 Fichier cible :  
`datasets/novfood_case_studies/S3_2_EcoPure_VN_48Mois.csv`


---

## 5. Travail demandé — Étapes détaillées

### Étape 1 — Visualisation + Analyse préliminaire

1. Charger les données dans Python (Pandas).  
2. Tracer la série temporelle.  
3. Décrire les patterns observés :  
   - sauts → changement de niveau ?  
   - tendance → linéaire ou non ?  
   - saisonnalité → faible / moyenne / forte ?

📌 **Question 1 :**  
Décrivez clairement si EcoPure Vietnam présente une **non-stationnarité** (niveau, variance ou saison).

---

### Étape 2 — Tests de stationnarité

Effectuer :

- ADF (Augmented Dickey-Fuller)  
- KPSS  

📌 **Question 2 :**  
Résultats des tests : la série est-elle stationnaire ?  
Faut-il différencier (d=1), log-transformer, stabiliser la variance ?

---

### Étape 3 — ACF / PACF → choix d’un premier modèle

1. Calculer ACF et PACF  
2. Proposer une première estimation de p, d, q  
3. Vérifier la saisonnalité annuelle (12 mois) → tester D=1 ou non

📌 **Question 3 :**  
Quels sont les ordres ARIMA(p, d, q) et SARIMA(P, D, Q, 12) proposés ?

---

### Étape 4 — Modélisation ARIMA sous Python

Utiliser `statsmodels` :

```python
from statsmodels.tsa.statespace.sarimax import SARIMAX

Tester :

ARIMA simple

SARIMA saisonnier (si D=1 pertinent)

Comparer les modèles :

AIC

BIC

Ljung-Box (résidus)

Normalité des résidus

📌 Question 4 :
Quel modèle est le meilleur statistiquement ? Justifiez avec AIC/BIC.

Étape 5 — Diagnostic des résidus

Tracer les résidus

Observer autocorrélation

Vérifier “white noise” (bruit blanc)

📌 Question 5 :
Les résidus sont-ils compatibles avec un bruit blanc ? (Justifiez avec ACF résidus)

Étape 6 — Prévision 12 mois & interprétation business

Générer le forecast 12 mois

Créer un graphique overlay :

historique 48 mois

prévision 12 mois

Écrire une narration business Vietnam claire et factuelle pour le S&OP.

📌 Question 6 :
Rédigez une note S&OP Vietnam (10 lignes) incluant :

tendance prévue,

risques identifiés,

saisonnalité,

impact sur production & logistique APAC.

6. Livrables attendus

Notebook Python complet avec tous les tests

Graphiques :

Série historique

ACF/PACF

Résidus

Forecast 12 mois

Tableau comparatif ARIMA / SARIMA

Note S&OP Vietnam (texte clair, non-technique)

7. Critères d’évaluation

Correctitude de la démarche statistique

Choix du modèle (justifié, pas arbitraire)

Qualité du notebook

Clarté de la narration business

Diagnostic des résidus (white noise obligatoire)

8. Extensions (niveau avancé)

Inclure Temp_Avg + Rainfall_mm → SARIMAX

Détection de changement de régime (changepoints)

ARIMA automatique (pmdarima)

Comparaison Holt-Winters vs ARIMA vs Prophet

Forecast probabiliste (IC 80% et 95%)

