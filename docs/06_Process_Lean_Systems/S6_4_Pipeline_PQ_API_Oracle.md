# Cas 6.4 — Pipeline Power Query → API → Oracle  
Automatisation complète Data → Forecast → ERP — NOVAFOOD GLOBAL

---

## 1. Résumé du cas

NOVAFOOD GLOBAL utilise **Oracle Demand Management Cloud (DMC)** pour gérer ses prévisions consolidées au niveau mondial.  
Cependant, les équipes Data & Demand Planning veulent :

- tirer parti de **Power Query** pour nettoyer 18 sources de données multi-pays,
- automatiser les étapes de transformation,
- générer un Forecast enrichi (MAPE / Bias / range forecast),
- **pousser automatiquement ce forecast** dans ORACLE via une **API REST**,
- valider la qualité avant écriture dans le système,
- intégrer le nouveau forecast dans le prochain cycle S&OP.

Vous êtes mandaté comme **Demand Planning Data Engineer** pour construire un **pipeline complet** :

> Power Query → Modèle Forecast → API Gateway → ORACLE DMC  
> + validation automatique + alarmes + logs

Ce pipeline doit être **sécurisé**, **répétable**, **audit-able**, **industrialisation-ready**.

---

## 2. Compétences visées

- Architecture Data Supply Chain  
- Power Query avancé  
- Transformation multi-sources à large échelle  
- API REST (POST / PUT / GET)  
- Normalisation du forecast pour Oracle  
- Validation qualité (QC)  
- Automatisation & scheduling  
- Documentation technique & fonctionnelle  

---

## 3. Périmètre NOVAFOOD

Sources de données utilisées (Europe + LATAM) :

- Ventes retail journalières  
- Données E-commerce (Amazon BR, MercadoLibre)  
- POS (France + Italie + Espagne)  
- Météo (API OpenWeather)  
- Master Data produit / SKU  
- Promotion calendar  
- Distribution numeric & weighted  
- Données Oracle existantes (forecast antérieurs)  

Forecasts générés :

- FreshBite EU  
- EcoPure France  
- NutriBox Maroc & Brésil  

Un pipeline unique doit gérer **32 000 SKU**, 18 pays, 6 canaux.

---

## 4. Travail demandé — Étapes détaillées

---

# 🔵 **Étape 1 — Power Query (Extraction & Transformation)**

Dans **Power Query**, construire un pipeline complet :

### A. Sources de données
Importer via :

- fichiers CSV bruts,  
- bases SQL,  
- API web (météo),  
- ORACLE extracts.

### B. Transformations essentielles
- Harmonisation des colonnes  
- Normalisation produits (SKU “global key”)  
- Nettoyage MDM (valeurs manquantes, doublons)  
- Jointures multi-pays  
- Table Fact_Demand NOVAFOOD  
- Dimensions (Product, Country, Channel, Calendar)

### C. Sortie Power Query
Créer une vue finale :

`VW_NOVFOOD_CLEAN_FORECAST_INPUT`

📌 **Question 1 : quelles transformations Power Query sont critiques pour assurer la qualité ?**

---

# 🔵 **Étape 2 — Modèle Forecast (Excel / Python / Power BI)**

Depuis `VW_NOVFOOD_CLEAN_FORECAST_INPUT` :

1. Calculer le *Forecast Base*  
2. Intégrer :
   - MAPE  
   - Bias  
   - P10 / P50 / P90  
3. Créer :
   - `Forecast_Final`  
   - `Forecast_Submission` (format Oracle)  

📌 **Question 2 : pourquoi faut-il une Key Figure spécifique “Forecast_Submission” pour Oracle ?**

---

# 🔵 **Étape 3 — Préparation des données pour API Oracle**

Conformer les données au format exigé par **Oracle DMC** :

Structure JSON recommandée :

```json
{
  "ForecastSubmission": {
    "Product": "FB-001",
    "Country": "FR",
    "Channel": "Retail",
    "Week": "2027-W15",
    "ForecastValue": 18290
  }
}


📌 Question 3 : quelles colonnes doivent être obligatoires dans la charge JSON ?

🔵 Étape 4 — Appel API (REST) vers Oracle

En Python :

import requests
import json

API_URL = "https://oracle.novfood.com/dmc/forecast"
HEADERS = {
    "Content-Type": "application/json",
    "Authorization": "Bearer <TOKEN>"
}

payload = {...}   # JSON construit par Power Query

response = requests.post(API_URL, data=json.dumps(payload), headers=HEADERS)

print(response.status_code, response.text)


Objectifs :

Envoi automatique

Gestion des erreurs

Log complet

📌 Question 4 : comment gérer un code erreur 409 (conflict) avec Oracle ?

🔵 Étape 5 — Validation & Contrôles Qualité

Contrôles obligatoires :

Total forecast ≠ 0

Valeurs négatives interdites

Vérifier cohérence vs Forecast Base

Contrôle de cohérence MDM

Vérifier horizon (max 24 mois)

Test API : dry-run avant submission finale

📌 Question 5 : quel contrôle qualité empêcherait d’écrire un forecast corrompu dans Oracle ?

🔵 Étape 6 — Scheduling (Automatisation)

Pipeline doit tourner :

chaque jour à 01h30

avant le job Oracle de consolidation

relance automatique si échec

Exemple YAML (pseudo-code) :

schedule: daily_0130
steps:
  - extract_powerquery
  - run_forecast_model
  - validate_data
  - send_to_oracle_api
  - generate_log
  - send_alert_email


📌 Question 6 : pourquoi l’étape validation doit-elle être avant l’appel API ?

🔵 Étape 7 — Génération des logs & alertes

Log obligatoire :

timestamp

SKU count envoyé

SKU en erreur

réponse API Oracle

utilisateur / machine

version pipeline

Alertes email :

taux d’erreurs

anomalies de volume

timeouts API

MAPE > seuil

📌 Question 7 : quels KPIs doivent figurer dans le log final ?

🔵 Étape 8 — Intégration S&OP

Le forecast soumis doit :

alimenter le Consensus Forecast,

être intégré au cycle S&OP France / Europe,

être visible via Power BI ou Oracle Analytics.

📌 Question 8 : comment intégrer le pipeline API dans le processus S&OP ?

🔵 Étape 9 — Documentation technique + fonctionnelle

À produire :

Architecture complète

Mapping Power Query

Structure JSON

Scénarios d’erreur API

Logs & alertes

Instructions S&OP

Plan d’audit

📌 Question 9 : quels éléments doivent figurer dans la documentation d’audit de fin de mois ?

5. Livrables attendus

Pipeline documenté

Script API

Vue Power Query

Forecast Submission file

Logs & rapport mensuel

Documentation technique & process

6. Critères d’évaluation

Robustesse du pipeline

Qualité du cleaning PQ

Respect format Oracle

Automatisation complète

Intégration S&OP fluide

Contrôles qualité pertinents

7. Extensions (niveau expert)

Trigger API via Power Automate

Monitoring temps réel

Double écriture Azure + Oracle

Forecast ML auto-adaptatif

Architecture serverless (Azure Functions)