# S1.2 — Master Data Management (MDM) : Correction de 2500 SKUs  
NOVAFOOD GLOBAL — Standardisation & Gouvernance Données

---

## 🎯 Objectif du cas

Corriger et standardiser un fichier MDM contenant **2500 SKUs pollués**, afin d’obtenir un référentiel produit propre, cohérent et utilisable dans :

- DAX  
- Power Query  
- SAP / Oracle  
- APS (Sofco / OMP / IBP)  

---

## 1. Dataset source

📂  
`datasets/novfood_raw/S1_2_MDM_2500_SKUs_raw.csv`

Contient anomalies :

- Codes SKU incohérents (Nutri, NUTRIBOX, nbx…)  
- Mauvais types (texte vs nombres)  
- Catégories manquantes  
- Marques incorrectes  
- Formats différents selon le pays  
- Description produit incomplète  
- Segmentation incohérente

---

## 2. Travail demandé

### 🔵 Étape 1 — Identifier & catégoriser les erreurs  
Créer un tableau :

| Type d’erreur | Volumes | Exemples |
|---------------|---------|----------|
| SKU incohérent | 560 | nbx1, nutribox 01 |
| Catégorie manquante | 210 | NULL |
| Code non conforme | 90 | 12121 / NAN |
| Caractères interdits | 30 | / ! & % |

---

### 🔵 Étape 2 — Appliquer le standard NOVAFOOD

Format SKU :

BRAND-CATEGORY-CODE
ex : NUTRIBOX-REG-001


Standardisation des marques :

| Input | Output |
|-------|--------|
| nutribox | NUTRIBOX |
| Nutri Box | NUTRIBOX |
| nbx | NUTRIBOX |

Catégories autorisées :

- REG  
- VEG  
- PRO  
- KIDS  

---

### 🔵 Étape 3 — Scripts de nettoyage (Power Query ou Python)

#### Exemple PQ :

```m
= Table.TransformColumns(#"Previous", {
    {"SKU", Text.Upper},
    {"Brand", Text.Proper},
    {"Category", each if _ = null then "REG" else _}
})

Exemple Python :
df["SKU"] = df["SKU"].str.upper().str.replace(" ", "-")
df["Brand"] = df["Brand"].replace(mapping_brand)

🔵 Étape 4 — Générer le master final

📄
datasets/novfood_cleaned/S1_2_MDM_2500_SKUs_clean.csv

Ajout colonne :

MDM_Status : OK / Warning / Error corrected

🔵 Étape 5 — Proposer un modèle de gouvernance MDM

Inclure :

rôles (DP, Data Owner, IT, Qualité)

règles de création SKU

workflow d’approbation

checklist création SKU

3. Livrables attendus

Fichier MDM propre

Rapport d’erreurs (Excel / Power BI)

Script PQ ou Python

Modèle de gouvernance

4. Critères d’évaluation

✔ MDM parfaitement propre
✔ Correction automatique et documentée
✔ Gouvernance robuste
✔ Aligné SAP / Oracle / IBP