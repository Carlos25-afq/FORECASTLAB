# 01 — Fundamentals of Supply Chain  
NOVAFOOD GLOBAL — Infrastructure, Flux & Gouvernance

La Supply Chain est l’ossature de NOVAFOOD GLOBAL, multinationale agroalimentaire opérant dans 18 pays avec plus de 32 000 SKU, 4 usines, 3 hubs logistiques et trois canaux principaux : Retail, E-commerce et Food Service.  
Cette section établit les fondations essentielles que tout Demand Planner doit maîtriser pour comprendre les flux, les contraintes et la gouvernance de bout en bout.

---

# 🎯 Objectifs de la section

À l’issue de cette section, vous serez capable de :

- Comprendre et cartographier les flux physiques et informationnels de la Supply Chain NOVAFOOD  
- Identifier les dépendances clés entre les opérations (Production, Achats, Qualité, Finance)  
- Manipuler et fiabiliser la **Master Data** pour assurer la cohérence du Demand Planning  
- Intégrer le fonctionnement complet d’un cycle **S&OP / IBP multinational**  
- Analyser les KPI financiers essentiels (BFR, marge, cash, coût complet)  
- Diagnostiquer les points de rupture qui affectent la prévision

---

# 🧩 1. Architecture Supply Chain de NOVAFOOD

La Supply Chain NOVAFOOD repose sur 4 piliers fondamentaux :

### **1.1 Production (Usines)**
- 🇫🇷 France → Produits frais & nutrition
- 🇲🇦 Maroc → Condiments, sauces, plats préparés
- 🇧🇷 Brésil → Snacks, produits innovants
- 🇻🇳 Vietnam → Ingrédients & extrusion

Contraintes majeures :  
- Capacité limitée  
- Calendrier maintenance  
- Lead time internes  
- Changements de format (changeovers)

### **1.2 Logistique Globale**
Hubs de consolidation :
- 🇧🇪 Belgique (UE)
- 🇰🇪 Kenya (Afrique)
- 🇲🇾 Malaisie (Asie)

Fonctions :  
- Buffer stocks  
- Cross-docking multi-pays  
- Support e-commerce

### **1.3 Distribution Multi-Canaux**
- **Retail** : Carrefour, Walmart, Auchan  
- **E-commerce** : Amazon, Jumia, MercadoLibre  
- **Food Service** : hôtels, restaurants, écoles

Chaque canal possède :  
- ses propres exigences  
- sa prévisibilité  
- ses cycles de promotions

### **1.4 Flux d’information**
- Prévisions → Production  
- Capacités → S&OP  
- MDM → ERP / APS  
- POS → Demand Sensing  
- Finance → Budget / landing / gap closing

---

# 🧩 2. Master Data Management (MDM)

Le Demand Planning repose sur une MDM **parfaite** :  
➡️ un seul code erroné = un mauvais forecast, un mauvais stock, un mauvais pilotage.

### Les données critiques :
- SKU  
- Hiérarchie produit  
- Famille / sous-famille / marque  
- Canal de distribution  
- Pays  
- Calendrier fiscal  
- Unités de mesure (UOM, pack, case, pallet)  
- Lead time  
- Statut produit (actif, neutre, fin de vie)

### Sources
- ERP (SAP, Oracle…)  
- CRM  
- WMS / TMS  
- Bases régionales pays

### Problèmes fréquents
- Doublons  
- Mauvais mapping  
- SKU obsolètes non archivés  
- Promo flags incohérents  
- Manque de hiérarchie

---

# 🧩 3. Le processus S&OP / IBP chez NOVAFOOD

Le S&OP (Sales & Operations Planning) aligne le **plan de demande**, le **plan de production**, et les **priorités financières**.

NOVAFOOD opère un S&OP **mensuel** et un IBP **trimestriel**.

### 3.1 Étapes S&OP mensuel

1. **Demand Review**  
   Analyse des drivers : prix, promos, innovations, météo

2. **Supply Review**  
   Capacité, besoins matière, CAPEX, import/export

3. **Pre-S&OP**  
   Alignement Finance / Demand / Supply

4. **Executive S&OP**  
   Arbitrages COMEX :  
   - risque de rupture  
   - allocation multi-pays  
   - priorisation production  
   - décisions marché

### 3.2 IBP trimestriel
- Mise à jour des hypothèses stratégiques  
- Ajustement du budget  
- Plan à 18 mois  
- Simulation Best/Base/Worst

---

# 🧩 4. KPI Financiers & Supply Chain

Le Demand Planner contribue directement à :

### 🔢 **BFR — Besoin en Fonds de Roulement**
- Stock moyen  
- Stock dormant  
- Obsolescence  
- Crédit fournisseurs / clients

### 💰 **Marge & Prix de Revient**
- Impact forecast → coût industriel  
- Gain/perte selon mix produit

### 📦 **Coûts logistiques**
- Transport inbound / outbound  
- Stockage  
- Manutention  
- Surstocks et pénalités distributeurs

### 🎯 **Service Client**
- OTIF  
- Fill rate  
- Taux de rupture

---

# 🧩 5. Points critiques affectant le Demand Planning

- Mauvaise qualité des données  
- Promotions mal anticipées  
- Décisions non alignées (Sales vs Supply)  
- Manque de visibilité sur capacité usine  
- Manque d’intégration ERP → APS  
- Flux internationaux lents ou instables  
- Mauvaise gestion des fins de vie produit

---

# 🧪 CAS PRATIQUES NOVAFOOD

## **1.1 : Cartographie globale de la Supply Chain NOVAFOOD**

🎯 Objectif :  
Créer une carte complète des flux (production → hubs → clients → retours)

Livrables :  
- Schéma Graphviz  
- Fichier JSON de la structure  
- Commentaire Supply Chain Manager

---

## **1.2 : Corriger un MDM pollué (2500 SKU)**  
Contexte :  
Le Maroc signale 2500 SKU corrompus (doublons, UOM incorrects)

🎯 Objectif :  
Nettoyer et standardiser un fichier MDM corrompu

Livrables :  
- Excel nettoyé  
- Rapport % erreurs corrigées  
- Recommandations MDM

---

## **1.3 : Reconstituer un cycle S&OP trimestriel**  
🎯 Objectif :  
Simuler un S&OP complet avec arbitrages multi-pays

Livrables :  
- Prévisions corrigées  
- Plans d’allocation  
- Présentation Executive S&OP

---

# 📌 Navigation

- [Section 2 — Data Tools for Demand Planners](../02_Data_Tools/index.md)
- [Retour au sommaire FORECASTLAB](../../README.md)

---
