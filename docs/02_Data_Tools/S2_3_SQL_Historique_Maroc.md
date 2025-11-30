# S2.3 — SQL : Reconstruction de l’Historique des Ventes Maroc  
NOVAFOOD GLOBAL — Consolidation Data & Fact_Demand_MA

---

## 🎯 Objectif du cas

Reconstituer une **table d’historique propre et complète** pour le Maroc à partir de plusieurs tables SQL hétérogènes :

- ventes brutes par canal,
- promotions,
- prix,
- référentiel produits,
- calendrier.

L’objectif final est de produire une table **`Fact_Demand_MA`** prête à être utilisée pour :

- le forecasting statistique,
- les analyses Power BI,
- les modèles avancés (causaux / ML),
- le processus S&OP NOVAFOOD Maroc.

---

## 1. Contexte & périmètre

NOVAFOOD Maroc vend principalement :

- **NutriBox**,  
- **EcoPure**,  
- **FreshBite**  

via 3 canaux :

- **Retail**,  
- **E-commerce**,  
- **Food Service**.

Les données sont réparties dans plusieurs tables SQL :

- `sales_maroc_retail`
- `sales_maroc_ecom`
- `sales_maroc_foodservice`
- `dim_product`
- `dim_customer`
- `dim_calendar`
- `price_maroc`
- `promo_maroc`

---

## 2. Structures des tables sources (exemple)

### 2.1. `sales_maroc_retail`

| Colonne        | Type       | Description                      |
|----------------|------------|----------------------------------|
| sale_date      | date       | Date de vente                    |
| sku_code       | varchar    | Code produit                     |
| customer_id    | int        | Enseigne / client                |
| units_sold     | int        | Quantité vendue                  |
| revenue        | decimal    | CA en MAD                        |

### 2.2. `sales_maroc_ecom`

| Colonne        | Type       |
|----------------|------------|
| order_date     | date       |
| sku            | varchar    |
| platform       | varchar    |
| units          | int        |
| net_sales_mad  | decimal    |

### 2.3. `sales_maroc_foodservice`

| Colonne        | Type       |
|----------------|------------|
| invoice_date   | date       |
| article        | varchar    |
| client_code    | int        |
| volume_kg      | decimal    |
| amount_mad     | decimal    |

### 2.4. Tables de référence

- `dim_product (sku, brand, category, segment, is_active, ...)`
- `dim_customer (customer_id, customer_name, channel, region, ...)`
- `dim_calendar (date, year, month, week, fiscal_period, ...)`
- `price_maroc (sku, date_start, date_end, list_price_mad, promo_price_mad, ...)`
- `promo_maroc (sku, customer_id, start_date, end_date, promo_type, discount_pct, ...)`

---

## 3. Travail demandé — Étapes SQL

---

### 🔹 Étape 1 — Normaliser les schémas de ventes

Créer trois vues intermédiaires pour uniformiser les colonnes.

#### 3.1. Ventes Retail

```sql
CREATE OR REPLACE VIEW v_sales_ma_retail AS
SELECT
    s.sale_date      AS tx_date,
    s.sku_code       AS sku,
    c.customer_id    AS customer_id,
    c.channel        AS channel,
    s.units_sold     AS units,
    s.revenue        AS revenue_mad
FROM sales_maroc_retail s
LEFT JOIN dim_customer c
    ON s.customer_id = c.customer_id;


3.2. Ventes E-commerce
CREATE OR REPLACE VIEW v_sales_ma_ecom AS
SELECT
    e.order_date     AS tx_date,
    e.sku            AS sku,
    NULL             AS customer_id,
    'ECOM'           AS channel,
    e.units          AS units,
    e.net_sales_mad  AS revenue_mad
FROM sales_maroc_ecom e;

3.3. Ventes Food Service
CREATE OR REPLACE VIEW v_sales_ma_foodservice AS
SELECT
    f.invoice_date   AS tx_date,
    f.article        AS sku,
    f.client_code    AS customer_id,
    'FOODSERVICE'    AS channel,
    f.volume_kg      AS units,
    f.amount_mad     AS revenue_mad
FROM sales_maroc_foodservice f;

🔹 Étape 2 — Union des canaux

Créer une vue consolidée :

CREATE OR REPLACE VIEW v_sales_ma_all AS
SELECT * FROM v_sales_ma_retail
UNION ALL
SELECT * FROM v_sales_ma_ecom
UNION ALL
SELECT * FROM v_sales_ma_foodservice;

🔹 Étape 3 — Jointure avec Dim_Product & Dim_Calendar
CREATE OR REPLACE VIEW v_sales_ma_enriched AS
SELECT
    c.date                 AS date,
    c.year                 AS year,
    c.month                AS month,
    s.sku,
    p.brand,
    p.category,
    p.segment,
    s.customer_id,
    s.channel,
    s.units,
    s.revenue_mad
FROM v_sales_ma_all s
LEFT JOIN dim_calendar c
    ON s.tx_date = c.date
LEFT JOIN dim_product p
    ON s.sku = p.sku;

🔹 Étape 4 — Intégration des prix et promotions
4.1. Joindre les prix
CREATE OR REPLACE VIEW v_sales_ma_price AS
SELECT
    v.*,
    pr.list_price_mad,
    pr.promo_price_mad
FROM v_sales_ma_enriched v
LEFT JOIN price_maroc pr
    ON v.sku = pr.sku
   AND v.date BETWEEN pr.date_start AND pr.date_end;

4.2. Joindre les promotions
CREATE OR REPLACE VIEW v_sales_ma_full AS
SELECT
    vp.*,
    CASE
        WHEN pm.sku IS NOT NULL
             AND vp.date BETWEEN pm.start_date AND pm.end_date
        THEN 1
        ELSE 0
    END AS promo_flag,
    pm.promo_type,
    pm.discount_pct
FROM v_sales_ma_price vp
LEFT JOIN promo_maroc pm
    ON vp.sku = pm.sku
   AND vp.customer_id = pm.customer_id
   AND vp.date BETWEEN pm.start_date AND pm.end_date;

🔹 Étape 5 — Création de la table Fact_Demand_MA
CREATE TABLE Fact_Demand_MA AS
SELECT
    date,
    year,
    month,
    sku,
    brand,
    category,
    segment,
    customer_id,
    channel,
    units,
    revenue_mad,
    list_price_mad,
    promo_price_mad,
    promo_flag,
    promo_type,
    discount_pct
FROM v_sales_ma_full;


Ajouter éventuellement une clé de substitution :

ALTER TABLE Fact_Demand_MA
ADD COLUMN demand_id BIGINT GENERATED ALWAYS AS IDENTITY;

🔹 Étape 6 — Contrôles de qualité

Requêtes de vérification :

Doublons potentiels

SELECT
    date, sku, channel, customer_id,
    COUNT(*) AS cnt
FROM Fact_Demand_MA
GROUP BY date, sku, channel, customer_id
HAVING COUNT(*) > 1;


Volumes négatifs ou aberrants

SELECT *
FROM Fact_Demand_MA
WHERE units < 0
   OR revenue_mad < 0;


Dates hors plage calendrier

SELECT *
FROM Fact_Demand_MA
WHERE year NOT BETWEEN 2018 AND 2030;

4. Livrables attendus

Table SQL :
Fact_Demand_MA dans le schéma de production/décisionnel.

Export analytique (pour Power BI / Python) :
datasets/novfood_cleaned/S2_3_Fact_Demand_Maroc.parquet

Script SQL complet :
datasets/generators/S2_3_SQL_Historique_Maroc.sql

Note technique :
docs/02_Data_Tools/S2_3_Notes_Techniques_Maroc.md
(explication des choix, hypothèses, limites).

5. Questions à traiter dans le cas

Quels sont les principaux risques de perte d’information lors de l’union des trois canaux ?

Comment gérer les cas où les prix sont manquants dans price_maroc ?

Que faire si certains SKU présents dans les ventes n’existent pas dans dim_product ?

Comment adapter la structure si l’on veut préparer un modèle causal prix–promo–distribution pour le Maroc ?

Quelle serait la meilleure clé de grain pour garantir l’unicité dans Fact_Demand_MA ?

6. Critères d’évaluation

Qualité du modèle de données final

Cohérence des jointures & des clés

Transparence des étapes SQL (commenté, structuré)

Absence de doublons / valeurs aberrantes

Adéquation au futur usage (forecasting & BI)