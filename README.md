# Zindi — Loan Default Prediction Challenge

> 🇫🇷 Une version française de ce README est disponible en bas de page.

---

## Context

This project is based on a Zindi machine learning challenge. The goal is to predict whether a loan applicant will repay their loan ("Good") or default ("Bad"), using demographic data and previous loan history. This type of model is commonly used by microfinance institutions and lenders to assess credit risk.

---

## Dataset

Three tables provided for both train and test sets:

| Table | Train | Test |
|---|---|---|
| Loan performance | 4,368 clients | 1,450 clients |
| Demographics | Client profile data | Client profile data |
| Previous loans | Historical loan records | Historical loan records |

**Class distribution (train set):**

| Class | Count |
|---|---|
| Good (repaid) | 3,416 |
| Bad (defaulted) | 952 |

The dataset is imbalanced — Good borrowers outnumber Bad borrowers by ~3.6:1.

---

## Methodology

**1. Multi-table merging**
The three train tables were merged on `customerid` to create a single training dataset combining loan performance, demographics, and borrowing history.

**2. Feature engineering on previous loans**
Aggregated historical loan data per client:
- Number of previous loans
- Average loan amount
- Average loan term (days)

**3. Target encoding**
Converted the text target (`Good` / `Bad`) into binary format: Good → 1, Bad → 0.

**4. Modelling**
Trained a Random Forest classifier. Class imbalance was acknowledged but not resampled — the model was trained on the raw distribution and evaluated using AUC-ROC, which is robust to class imbalance.

---

## Results

| Metric | Score |
|---|---|
| AUC-ROC | 0.65 |

---

## Tech stack

- Python
- pandas, numpy
- scikit-learn (RandomForestClassifier)

---

## Key decisions

- AUC-ROC chosen as the evaluation metric — more reliable than accuracy on imbalanced datasets
- No SMOTE applied — class imbalance handled implicitly through metric selection
- Non-predictive identifiers (`customerid`, `systemloanid`) excluded from features

---
---

# Zindi — Prédiction du Défaut de Remboursement de Prêt

## Contexte

Ce projet est basé sur un challenge Zindi de machine learning. L'objectif est de prédire si un emprunteur remboursera son prêt ("Good") ou fera défaut ("Bad"), à partir de données démographiques et d'un historique de prêts antérieurs. Ce type de modèle est couramment utilisé par les institutions de microfinance pour évaluer le risque de crédit.

---

## Données

Trois tables fournies pour les ensembles d'entraînement et de test :

| Table | Train | Test |
|---|---|---|
| Performance des prêts | 4 368 clients | 1 450 clients |
| Démographie | Profil client | Profil client |
| Prêts antérieurs | Historique des emprunts | Historique des emprunts |

**Distribution des classes (ensemble d'entraînement) :**

| Classe | Nombre |
|---|---|
| Good (remboursé) | 3 416 |
| Bad (défaut) | 952 |

Le dataset est déséquilibré — les bons emprunteurs sont ~3,6 fois plus nombreux que les mauvais.

---

## Méthodologie

**1. Fusion multi-tables**
Les trois tables d'entraînement ont été fusionnées sur `customerid` pour créer un dataset unique combinant performance, démographie et historique d'emprunt.

**2. Feature engineering sur les prêts antérieurs**
Agrégation des données historiques par client :
- Nombre de prêts antérieurs
- Montant moyen des prêts
- Durée moyenne des prêts (en jours)

**3. Encodage de la cible**
Conversion de la variable cible textuelle (`Good` / `Bad`) en format binaire : Good → 1, Bad → 0.

**4. Modélisation**
Entraînement d'un classificateur Random Forest. Le déséquilibre des classes a été pris en compte dans le choix de la métrique plutôt que par rééchantillonnage.

---

## Résultats

| Métrique | Score |
|---|---|
| AUC-ROC | 0.65 |

---

## Stack technique

- Python
- pandas, numpy
- scikit-learn (RandomForestClassifier)

---

## Décisions clés

- AUC-ROC retenu comme métrique — plus fiable que l'accuracy sur des données déséquilibrées
- Pas de SMOTE appliqué — le déséquilibre des classes est géré implicitement par le choix de la métrique
- Identifiants non prédictifs (`customerid`, `systemloanid`) exclus des features
