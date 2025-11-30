# S2.2 — Dashboard Power BI : Forecast vs Actuals (Europe)
NOVAFOOD GLOBAL — Performance Prévisionnelle & Analyse Multi-Pays

---

## 🎯 Objectif du cas

Construire un **dashboard Power BI professionnel** permettant à NOVAFOOD Europe de :

- comparer **Forecast vs Actuals** par pays, SKU, catégorie et canal,
- calculer automatiquement les principaux **indicateurs d’erreur** (MAPE, Biais, WAPE, RMSE),
- analyser la performance par **pays / gamme / canal**,
- fournir un support visuel au **processus S&OP Europe**.

Le dashboard doit être :

- robuste (capable de gérer **> 1 million de lignes**),
- lisible par le COMEX,
- actionnable pour le Demand Planner et l’équipe S&OP.

---

## 1. Dataset utilisé

📂 Fichier :  
`datasets/novfood_cleaned/S2_2_FcastActuals_EU.parquet`

Colonnes de base :

| Colonne          | Description                                         |
|------------------|-----------------------------------------------------|
| Date             | Date de vente / forecast (format YYYY-MM-DD)       |
| Country          | FR, DE, ES, IT, BE, NL, …                           |
| SKU              | Code produit NOVAFOOD standardisé                  |
| Category         | NutriBox / EcoPure / FreshBite / VitalMeal         |
| Channel          | Retail / Ecom / FoodService                        |
| Actuals          | Ventes réelles                                     |
| Forecast         | Prévision statistique / consensus                  |
| Consensus_Fcst   | (optionnel) Forecast final S&OP                    |
| Promo_Flag       | 0 / 1                                              |
| Price            | Prix de vente consommateur                         |

Objectif : construire le modèle de données, les **mesures DAX**, et le **rapport complet**.

---

## 2. Étapes détaillées

---

### 🔹 Étape 1 — Importer le dataset dans Power BI

1. Ouvrir **Power BI Desktop**  
2. `Obtenir des données` → `Parquet`  
3. Sélectionner : `S2_2_FcastActuals_EU.parquet`  
4. Vérifier les types de données :

   - `Date` → Date  
   - `Actuals`, `Forecast`, `Price` → Decimal Number  
   - `Country`, `SKU`, `Category`, `Channel` → Texte

---

### 🔹 Étape 2 — Créer le modèle de données

#### 2.1. Créer une table de dates (Dim_Date)

Dans `Modélisation` → `Nouvelle table` :

```DAX
Dim_Date =
ADDCOLUMNS (
    CALENDAR (DATE(2018,1,1), DATE(2030,12,31)),
    "Year", YEAR ( [Date] ),
    "MonthNum", MONTH ( [Date] ),
    "Month", FORMAT ( [Date], "MMM" ),
    "YearMonth", FORMAT ( [Date], "YYYY-MM" ),
    "Quarter", "Q" & FORMAT ( [Date], "Q" )
)


2.2. Créer une dimension produit (Dim_Product)

Dans Modélisation → Nouvelle table :

Dim_Product =
DISTINCT (
    SELECTCOLUMNS (
        Fact_FcastActuals,
        "SKU", Fact_FcastActuals[SKU],
        "Category", Fact_FcastActuals[Category]
    )
)


(Supposons que la table importée s’appelle Fact_FcastActuals.)

2.3. Relations

Dim_Date[Date] → Fact_FcastActuals[Date] (1 → *)

Dim_Product[SKU] → Fact_FcastActuals[SKU] (1 → *)

Direction : simple (Dim → Fact).

🔹 Étape 3 — Créer les mesures DAX clés

Dans Fact_FcastActuals, créer les mesures suivantes :

3.1. Total Actuals
Total_Actuals :=
SUM ( Fact_FcastActuals[Actuals] )

3.2. Total Forecast
Total_Forecast :=
SUM ( Fact_FcastActuals[Forecast] )

3.3. Erreur Absolue Agrégée
Abs_Error :=
SUMX (
    Fact_FcastActuals,
    ABS ( Fact_FcastActuals[Actuals] - Fact_FcastActuals[Forecast] )
)

3.4. MAPE (en %)
MAPE :=
DIVIDE (
    [Abs_Error],
    [Total_Actuals]
)


(à formater en %)

3.5. Biais (%)
Bias :=
DIVIDE (
    [Total_Forecast] - [Total_Actuals],
    [Total_Actuals]
)

3.6. WAPE
WAPE :=
DIVIDE (
    [Abs_Error],
    [Total_Actuals]
)


(souvent identique au MAPE agrégé, mais on sépare pour clarté métier)

3.7. RMSE
RMSE :=
VAR n =
    COUNTROWS ( Fact_FcastActuals )
VAR mse =
    DIVIDE (
        SUMX (
            Fact_FcastActuals,
            POWER ( Fact_FcastActuals[Forecast] - Fact_FcastActuals[Actuals], 2 )
        ),
        n
    )
RETURN
    SQRT ( mse )

🔹 Étape 4 — Construire le dashboard
4.1. Zone KPI (en haut de la page)

Créer 4 cartes :

Carte 1 : MAPE

Carte 2 : Bias

Carte 3 : WAPE

Carte 4 : RMSE

Ajouter des slicers :

Country

Category

Channel

Year

Month

4.2. Courbe Forecast vs Actuals dans le temps

Visuel : Line Chart

Axe X : Dim_Date[Date]

Valeurs :

Ligne 1 : [Total_Actuals]

Ligne 2 : [Total_Forecast]

Légende : Country (optionnel)

Filtres : slicers créés précédemment.

4.3. Table “Top Erreurs SKU”

Visuel : Table

Colonnes :

SKU

Category

Country

[Total_Actuals]

[Total_Forecast]

[Abs_Error]

[MAPE]

Tri décroissant sur [Abs_Error].

4.4. Heatmap par pays (MAPE Europe)

Visuel : Filled Map

Localisation : Country

Valeur : [MAPE]

Couleur conditionnelle : du vert (bon) au rouge (mauvais).

4.5. Graphique “Error vs Promo”

Visuel : Clustered Column Chart

Axe X : Promo_Flag

Valeurs : [MAPE] ou [WAPE]

Objectif : montrer si les promotions dégradent la qualité de la prévision.

🔹 Étape 5 — Export S&OP & rafraîchissement

Sauvegarder le fichier sous :
excel_templates/S2_2/Forecast_vs_Actuals_EU.pbix

Publier dans Power BI Service (workspace “NOVAFOOD_SOP”).

Configurer un rafraîchissement quotidien (02h00).

Optionnel : activer RLS (Row Level Security) :

Rôle Country_Manager : ne voit que son pays

Rôle EU_SOP : voit toute l’Europe

3. Livrables attendus

Fichier Power BI :
excel_templates/S2_2/Forecast_vs_Actuals_EU.pbix

Script DAX documenté :
excel_templates/DAX_measures/S2_2_DAX_Fcast_vs_Actuals.txt

Documentation utilisateur (S&OP) :
docs/02_Data_Tools/S2_2_UserGuide.md

4. Critères d’évaluation

Exactitude des mesures DAX (MAPE, Biais, WAPE, RMSE)

Clarté du dashboard (lecture en moins de 30 secondes par un directeur)

Capacité à filtrer par pays / gamme / canal / temps

Stabilité des visuels même avec de gros volumes de données

Alignement avec les besoins du processus S&OP NOVAFOOD Europe