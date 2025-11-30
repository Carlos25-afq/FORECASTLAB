# 08 — Ethics & Responsible AI in Forecasting  
NOVAFOOD GLOBAL — Gouvernance Algorithmique, Biais, Transparence & Sécurité

L’intégration du Machine Learning dans la prévision apporte puissance et rapidité, mais elle introduit aussi des risques : biais, opacité, erreurs d'interprétation, dérives éthiques, décisions non explicables.  
Chez NOVAFOOD GLOBAL, chaque modèle statistique ou ML est évalué sous l’angle **éthique**, **organisationnel**, **algorithme**, et **impact Supply Chain / client final**.

---

# 🎯 Objectifs de la section

À la fin de cette section, vous serez capable de :

- Identifier les biais courants dans les modèles de prévision  
- Comprendre les risques éthiques associés aux algorithmes en Supply Chain  
- Mettre en place une gouvernance robuste pour les modèles ML  
- Gérer la transparence, l’auditabilité et l’explicabilité  
- Éviter les dérives dans les décisions automatiques  
- Mettre en place des garde-fous lors du Demand Sensing ou des promotions  
- Intégrer la notion d’équité et d’impact consommateur  

---

# 🧩 1. Les risques éthiques en Demand Planning & ML

### 1.1 Biais algorithmiques
Les modèles ML peuvent amplifier des injustices, par exemple :
- surpondération des magasins Premium  
- surévaluation du e-commerce par rapport au retail  
- biais sur certaines régions (ex : Afrique vs EU)  
- effet "sur-promo" appris par les algorithmes

### 1.2 Décisions opaques
Un modèle black-box peut :
- sur-prévoir, entraînant surstock  
- sous-prévoir, entraînant ruptures  
- surévaluer un segment client  
- ignorer des ruptures logistiques réelles  

### 1.3 Risques supply chain
- Ruptures artificielles  
- Mauvaises allocations multi-pays  
- Mauvaise priorisation production  
- Perte de marge  
- Mauvaise gestion du BFR  

---

# 🧩 2. Gouvernance Algorithmique NOVAFOOD

NOVAFOOD a mis en place un cadre strict de gouvernance :

### 2.1 Documentation obligatoire
Chaque modèle doit avoir :
- dataset utilisé  
- variables explicatives  
- justification des features   
- responsable du modèle  
- portée (pays / produits)

### 2.2 Validation multi-fonctionnelle
Modèles validés conjointement par :
- Demand Planning  
- Sales  
- Finance  
- IT Data / APS  
- Qualité  

### 2.3 Cycle de vie du modèle
1. Développement  
2. Test / validation  
3. Déploiement  
4. Monitoring  
5. Retrait ou amélioration  

---

# 🧩 3. Transparence & Explicabilité

### Outils utilisés :
- SHAP values  
- Partial Dependence Plots  
- Importance des variables  
- Residual analysis  
- Modèles hybrides interpretable-first

Objectif :  
➡️ comprendre *pourquoi* le modèle recommande une prévision.

---

# 🧩 4. Sécurité & Prévention des dérives

### 4.1 Garde-fous NOVAFOOD
- seuils d’alerte si variation > +/- 25%  
- revue hebdomadaire avec Demand Planning  
- interdiction de décisions 100% automatiques  
- obligation de justification en S&OP  

### 4.2 Prévention des mauvaises pratiques
- pas de ré-entraînement automatique sans validation  
- interdiction de modèles mono-variable (trop fragiles)  
- contrôle qualité dataset avant ingestion  

---

# 🧩 5. AI & Impact Sociétal

NOVAFOOD opère dans 18 pays avec des niveaux économiques variés.  
Les choix algorithmiques peuvent impacter :

- disponibilité des produits essentiels  
- prix consommateurs  
- rupture dans zones sensibles  
- inclusion numérique des petits distributeurs  
- sécurité alimentaire (Food Security)

➡️ L’IA ne doit JAMAIS générer d’inégalités entre marchés.

---

# 🧪 CAS PRATIQUES NOVAFOOD

---

## **8.1 : Détecter un biais ML dans le modèle promo Brésil**
🎯 Objectif :  
Analyser et corriger un modèle ML qui sous-estime systématiquement les régions à faible revenu.

Livrables :
- Analyse SHAP  
- Tableau biais corrigé  
- Nouvelle version du modèle

---

## **8.2 : Créer un modèle explicable & responsable**
🎯 Objectif :  
Construire un modèle XGBoost version “Explainable First”.

Livrables :
- Notebook Python  
- SHAP + PDP  
- Guide de décision S&OP

---

# 📌 Navigation

- [Retour au sommaire FORECASTLAB](../../README.md)

---
