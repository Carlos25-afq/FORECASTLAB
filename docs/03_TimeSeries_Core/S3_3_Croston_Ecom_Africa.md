# Cas 3.3 — Demande intermittente E-commerce Afrique : Méthodes Croston, SBA et TSB  
NOVAFOOD GLOBAL — Forecasting longue traîne E-commerce

---

## 1. Résumé du cas

FreshBite Accessory Line est la gamme d’accessoires E-commerce vendus dans plusieurs pays africains : Kenya, Côte d’Ivoire, Nigeria, Afrique du Sud.

Ces produits ont une **demande avec beaucoup de zéros**, des pics irréguliers et aucune saisonnalité claire.  
La demande intermittente représente **40% du portefeuille E-commerce** de NOVAFOOD GLOBAL et influence :

- la planification E-commerce,
- les réapprovisionnements micro-logistiques,
- les coûts de stockage,
- les taux de rupture.

Votre mission : construire un **forecast réaliste** à partir de données irrégulières (36 mois), en utilisant :

- Croston classique  
- SBA (Syntetos-Boylan Approximation)  
- TSB (Teunter-Syntetos-Babai)  

Et formuler une recommandation pour le pilotage de stock E-commerce.

---

## 2. Compétences visées

- Identifier la demande intermittente vs lisse  
- Comprendre les limites des méthodes classiques (MA, SES)  
- Implémenter Croston / SBA / TSB dans Excel ou Python  
- Calculer des fréquences & tailles moyennes  
- Choisir un modèle adapté au E-commerce longue traîne  
- Rédiger une recommandation stock + forecast orientée business

---

## 3. Contexte NOVAFOOD — E-commerce Afrique

Les données concernent un SKU E-commerce vendu dans 4 marchés :

- Kenya  
- Côte d’Ivoire  
- Nigeria  
- Afrique du Sud  

Chaque SKU connaît :

- des longueurs de séries irrégulières,  
- des mois sans ventes,  
- des campagnes flash,  
- de fortes variations de fréquence.

Ce cas te met dans le rôle du **Demand Planner Africa E-commerce**.

---

## 4. Jeu de données

📂 Dataset cible :  
`datasets/novfood_case_studies/S3_3_Ecom_Africa_Intermittent.csv`



---

## 5. Travail demandé — Étapes détaillées

### Étape 1 — Analyse de l’intermittence

1. Importer les données.  
2. Calculer pour chaque pays :
   - fréquence de demande = % de mois avec vente  
   - taille moyenne des ventes non nulles  
   - CV (coefficient de variation)  

📌 **Question 1 :**  
Classez les 4 pays du plus “prévisible” au plus “intermittent”. Justifiez.

---

### Étape 2 — Test des méthodes classiques (à montrer que ça échoue)

1. Moving Average (3 / 6 / 12 mois)  
2. SES (Simple Exponential Smoothing)

📌 **Question 2 :**  
Pourquoi les méthodes classiques sous-performent-elles sur cette série ?

---

### Étape 3 — Implémentation Croston (original)

1. Séparer :
   - intervalles (temps entre ventes ≠ 0)  
   - tailles de demande  
2. Appliquer Croston :
   - lissage α  
   - fréquence & taille séparées  
3. Calculer la prévision finale.

📌 **Question 3 :**  
Montrez la mise à jour (t+1) pour les mois 11, 17, 25, 29 et 34 (comme dans le cours).

---

### Étape 4 — Implémentation SBA (Syntetos-Boylan)

1. Appliquer le correctif (1 - α/2)  
2. Calculer le forecast final.

📌 **Question 4 :**  
SBA corrige un biais majeur de Croston.  
Expliquez en 4–5 lignes.

---

### Étape 5 — Implémentation TSB (Teunter-Syntetos-Babai)

1. Estimer :
   - probabilité de demande (p)  
   - taille moyenne  
2. Mettre à jour p avec lissage β  
3. Calculer le forecast final.

📌 **Question 5 :**  
En quoi TSB est mieux adapté lorsqu’il y a des périodes prolongées de zéro ?

---

### Étape 6 — Comparaison des méthodes

Comparer :  
- Croston  
- SBA  
- TSB  
- (optionnel) SES / MA  
en termes de :

- MASE  
- RMSE  
- Forecast Bias  
- Interprétabilité  
- Capacité à anticiper longues périodes de zéro  

📌 **Question 6 :**  
Quel modèle recommandez-vous pour E-commerce Kenya ? Et pour Nigeria ? Justifiez.

---

### Étape 7 — Recommandations Stock & S&OP

Pour chaque pays :

- définir une stratégie de stock  
- proposer des règles business :
  - min-max  
  - review périodique  
  - MOQ  
  - différenciation selon l’intermittence

📌 **Question 7 :**  
Écrivez une note au S&OP Africa expliquant la stratégie de stock pour ce SKU.

---

## 6. Livrables attendus

- Excel ou notebook avec :  
  - Croston  
  - SBA  
  - TSB  
  - comparatifs  
- Graphiques (historiques + forecast)  
- Résumé multipays  
- Note S&OP Africa E-commerce  

---

## 7. Critères d’évaluation

- Correctitude des implémentations  
- Cohérence dans la segmentation (pays)  
- Qualité des comparaisons  
- Pertinence des recommandations stock  
- Clarté de la narration business  

---

## 8. Extensions (niveau expert)

- Implémenter **Intermittent Prophet (MAP-PROP)**  
- Ajouter météo / prix → Croston modifié  
- Détection de “zéro atrophique”  
- Approche Bayesian Croston  

---
