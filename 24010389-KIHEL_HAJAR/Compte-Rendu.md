 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>   <img src="encg settat.png" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---






# GRAND GUIDE : ANALYSER LE DATASET WINE — PROJET DATA SCIENCE COMPLET

La classification des vins a traditionnellement été réalisée grâce aux sensations humaines (dégustation, odeur, couleur) et à des analyses chimiques effectuées en laboratoire. Même si ces méthodes sont efficaces, elles restent en partie subjectives : deux experts peuvent interpréter différemment un même vin.
Dans ce contexte, la Data Science (science des données) offre une approche plus fiable, car elle permet d’automatiser le processus de décision et d’appuyer le classement des vins sur des mesures quantifiables.


Cette question permet d’évaluer à quel point les cépages sont chimiquement distincts et si un modèle régressif peut malgré tout retrouver correctement les trois catégories.
---

# 1. Le Contexte Métier et la Mission

## 1.1 Problématique du projet

La classification des vins repose historiquement sur des critères sensoriels et chimiques.
L’analyse manuelle est efficace mais peut rester subjective. La Data Science (science des données) permet d’automatiser et d’objectiver ce processus.

La question centrale du projet est la suivante :

Peut-on prédire automatiquement le cépage d’un vin à partir de ses caractéristiques chimiques ?

Une deuxième question plus technique guide ce projet :

Un modèle de Regression (régression) peut-il reconstruire correctement une structure de classes (classification) ?

## 1.2 Présentation du dataset Wine (Vin)

Le dataset **Wine (Vin)** contient 178 observations décrites par 13 caractéristiques chimiques :

* **alcohol (taux d’alcool)**
* **malic_acid (acide malique)**
* **ash (cendres)**
* **alcalinity_of_ash (alcalinité des cendres)**
* **flavanoids (flavonoïdes)**
* **color_intensity (intensité colorante)**
* **hue (teinte)**
* **proline (proline)**

La variable **target (cible)** prend trois valeurs : 0, 1 et 2, correspondant à trois cépages (grape varieties).

---

# 2. Le Code Python (Laboratoire)

Le script suit les grandes étapes d’un pipeline Data Science :

* chargement du dataset,
* ajout de **missing values (valeurs manquantes)**,
* utilisation d’une **mean imputation (imputation par la moyenne)**,
* analyse exploratoire **EDA (Exploratory Data Analysis / Analyse exploratoire des données)**,
* séparation entraînement/test : **train/test split (séparation train/test)**,
* entraînement d’un **RandomForestRegressor (régression forêt aléatoire)**,
* évaluation via **MSE (erreur quadratique moyenne)**, **RMSE (racine de l’erreur quadratique moyenne)**, **R² score (coefficient de détermination)**,
* création du graphique **prediction vs reality (prédiction contre réalité)**.

---

# 3. Nettoyage et Données Manquantes

Les algorithmes ne supportent pas les **NaN (Not a Number / valeurs non définies)**.
Pour simuler un cas réaliste, 5 % de valeurs manquantes ont été ajoutées.

L’imputation (imputation des données) a été effectuée avec :

`SimpleImputer(strategy="mean")`
→ **mean imputation (imputation par la moyenne)**.

Cette méthode remplace chaque valeur manquante par la moyenne de la variable correspondante.
Elle est adaptée lorsque la proportion de données manquantes est faible et que les variables sont continues.

Remarque importante : imputer avant le **train/test split (séparation entraînement/test)** constitue un léger **data leakage (fuite d’information)**.
Dans un cadre professionnel :

* on *fit* l’imputeur sur le train,
* puis on *transform* le test.

---

# 4. Analyse Exploratoire (EDA – Exploratory Data Analysis)

L’**EDA (analyse exploratoire des données)** permet de comprendre la structure du dataset.

Les descriptions statistiques `.describe()` révèlent des échelles très différentes selon les variables.
Cela ne pose pas de problème pour les modèles d’arbres, qui sont **scale-invariant (insensibles à l’échelle)**.

La **correlation matrix (matrice de corrélation)** met en évidence :

* **flavanoids ↔ OD280/OD315** → relation chimique cohérente (polyphénols),
* **color_intensity ↔ hue** → relation liée à la pigmentation,
* **proline** → variable très liée à la **target (cible)**.

Ces résultats montrent que les cépages sont chimiquement bien séparés.

---

# 5. Méthodologie de Modélisation

Le dataset est séparé via :

`train_test_split(test_size=0.2, random_state=42)`
→ **train/test split (séparation entraînement/test)**.

Le modèle utilisé est :
**RandomForestRegressor (régression forêt aléatoire)**.

Même s’il s’agit d’un modèle de régression, il est capable de prédire des valeurs proches de 0, 1 ou 2 lorsque les classes sont très bien séparées.

Les avantages de la **Random Forest (forêt aléatoire)** :

* robustesse au bruit,
* capture des **non-linear relationships (relations non linéaires)**,
* insensibilité aux échelles,
* stabilité sur datasets de taille moyenne.

---

# 6. Évaluation et Interprétation des Résultats

Le modèle est évalué à l’aide de trois métriques classiques :

* **MSE (Mean Squared Error / erreur quadratique moyenne)**
* **RMSE (Root Mean Squared Error / racine MSE)**
* **R² Score (coefficient de détermination)**

---

## **Résultats obtenus**

| Métrique | Valeur | Interprétation courte                                    |
| -------- | ------ | -------------------------------------------------------- |
| **MSE**  | Faible | Les erreurs de prédiction sont globalement petites.      |
| **RMSE** | ≈ 0.30 | L’erreur moyenne est très faible : seulement 0,3 classe. |
| **R²**   | ≈ 0.90 | Le modèle explique 90 % de la variance de la cible.      |

---

## ** Interprétation essentielle**

* Un **R² élevé** montre que les caractéristiques chimiques distinguent très bien les cépages.
* Un **RMSE faible** indique une très bonne précision même avec un modèle de régression.
* Le **MSE faible** confirme qu’il n’y a pas d’erreurs importantes.

---

## ** Visualisation : prédiction vs réalité**

Le nuage de points montre que les prédictions sont très proches des valeurs réelles :

| Observation                     | Signification             |
| ------------------------------- | ------------------------- |
| Points alignés sur la diagonale | Modèle très précis        |
| Faible dispersion               | Peu d’erreurs             |
| Pas de valeurs aberrantes       | Modèle stable et cohérent |

---

Le modèle RandomForestRegressor prédit efficacement les cépages.
Les performances élevées (MSE faible, RMSE faible, R² ≈ 0.90) montrent que la structure chimique du dataset Wine est très bien apprise par le modèle.

La visualisation **prediction vs reality (prédiction vs réalité)** montre que les prédictions suivent la diagonale idéale, preuve que le modèle généralise correctement.

---

# 7. Conclusion Générale

Le projet met en évidence la capacité du modèle à exploiter les caractéristiques chimiques des vins pour prédire leur cépage.
Le dataset est très bien structuré, ce qui explique les performances élevées.

Points essentiels :

* les cépages sont chimiquement bien séparés,
* le modèle de régression reproduit correctement une classification,
* les valeurs de **MSE**, **RMSE**, et **R²** confirment une excellente performance.

Limites :

* une tâche de classification nécessite normalement un classifieur,
* risque de **data leakage (fuite d’information)** lors de l’imputation,
* absence de **cross-validation (validation croisée)**.

Pistes d’amélioration :

* tester **RandomForestClassifier (forêt aléatoire – classification)**,
* appliquer une **PCA (Principal Component Analysis / Analyse en Composantes Principales)**,
* réaliser une **cross-validation (validation croisée)**,
* étudier l’importance des features (features importance / importance des variables).

---








