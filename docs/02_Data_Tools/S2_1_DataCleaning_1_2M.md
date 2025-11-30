# S2.1 — Data Cleaning Avancé (1,2 million de lignes)  
NOVAFOOD GLOBAL — Pipeline Power Query + Data Engineering

---

## 🎯 Objectif du cas
Nettoyer, structurer et normaliser un dataset brut de **1,2 million de lignes** provenant :

- de 18 pays,
- de 3 canaux (Retail, E-commerce, Food Service),
- de 4 usines,
- avec des problèmes réels : doublons, formats incohérents, devises multiples, SKU mal codifiés.

Ce cas simule un nettoyage professionnel **avant modélisation**.

---

# 1. Dataset source

📂 Localisation :  
`datasets/novfood_raw/S2_1_raw_1_2M.csv`

Colonnes présentes :

| Colonne | Description |
|--------|-------------|
| Date | format mixte (YYYY-MM-DD, DD/MM/YYYY, texte) |
| Country | FR, MA, BR, VN, EU… |
| SKU | codes variés (NBX-001, NUTRIBOX-1, nutribox1, etc.) |
| Channel | retail, ecom, foodservice |
| Units_Sold | ventes (mais valeurs manquantes + valeurs aberrantes) |
| Price | prix (€, MAD, BRL, VND mélangés) |
| Currency | EUR, MAD, BRL, VND |
| Promo_Flag | différents formats (0/1, TRUE/FALSE, Oui/Non) |
| Customer_ID | facultatif, parfois vide |

---

# 2. Travail demandé

## 🔵 **Étape 1 — Charger le dataset dans Power Query**
- Importer le CSV
- Inspecter les types
- Identifier les erreurs

---

## 🔵 **Étape 2 — Harmoniser les dates**
Contient 3 formats différents.

Transformation Power Query à appliquer :

```m
= Table.TransformColumns(#"Source",{ "Date", each Date.From(_) })

🔵 Étape 3 — Normaliser les SKU (standard NOVAFOOD)

Objectif :
Tous les SKU doivent être en format standard :

MARQUE-CATÉGORIE-CODE
ex : NUTRIBOX-REG-001


Power Query :

mettre en majuscule

remplacer espaces par tirets

nettoyer caractères spéciaux

appliquer table de mapping SKU maître

🔵 Étape 4 — Convertir toutes les devises en EUR

Utiliser le fichier :

📄 datasets/novfood_case_studies/S2_1_fx_rates.csv

Exemple M :

= Table.AddColumn(#"Previous", "Price_EUR", each [Price] * fx_rate, type number)

🔵 Étape 5 — Nettoyer les valeurs aberrantes

Units_Sold négatifs → corriger ou supprimer

Prix > 200 € → signaler en anomalie

Promo_Flag incohérent → standardiser

Créer un rapport d’anomalies :

📄 datasets/novfood_cleaned/S2_1_anomalies.xlsx

🔵 Étape 6 — Dédupliquer

Clés :

Date + Country + SKU + Channel

3. Livrables attendus

📁 Fichier final propre :
datasets/novfood_cleaned/S2_1_clean_1_2M.parquet

📁 Rapport anomalies :
datasets/novfood_cleaned/S2_1_anomalies.xlsx

📁 Code complet Power Query :
excel_templates/PowerQuery/S2_1_PQ_Code.txt

4. Critères d’évaluation

✔ Qualité du nettoyage
✔ Transparence des transformations
✔ Absence totale de doublons
✔ Uniformité SKU / dates / devises
✔ Structure prête pour DAX & machine learning