

# **Compte rendu d’Analyse : Étude et Modélisation de l’Évolution de la Pandémie Covid-19 par Méthodes de Régression**

**Date :** 30 Novembre 2025
**Auteur :** *Analyse Covid-19*

---
## **Table des matières**

1. [Introduction](#introduction)
2. [Importation des librairies](#importation-des-librairies)
3. [Chargement du jeu de données](#chargement-du-jeu-de-données)
4. [Analyse exploratoire du dataset](#analyse-exploratoire-du-dataset)
5. [Prétraitement et Feature Engineering](#prétraitement-et-feature-engineering)
6. [Analyse descriptive et visualisations](#analyse-descriptive-et-visualisations)
7. [Méthodologie de modélisation](#méthodologie-de-modélisation)
8. [Régression Linéaire](#régression-linéaire)
9. [Régression Polynomiale](#régression-polynomiale)
10. [Arbre de Décision](#arbre-de-décision)
11. [Forêt Aléatoire](#forêt-aléatoire)
12. [Support Vector Regression (SVR)](#support-vector-regression-svr)
13. [Comparaison globale des modèles](#comparaison-globale-des-modèles)
14. [Conclusion générale](#conclusion-générale)


# Analyse de la Pandémie Covid‑19 – Compte Rendu Complet

## 1. Introduction (Contexte Général)

La pandémie de Covid‑19, apparue à la fin de l’année 2019, a provoqué une crise sanitaire mondiale sans précédent. Comprendre son évolution à travers les données quantitatives permet non seulement d'analyser la dynamique de propagation du virus, mais aussi de mesurer l’impact des politiques publiques, des comportements sociaux et des mesures préventives. Ce rapport présente une analyse complète et structurée du dataset Covid‑19 à travers plusieurs méthodes statistiques et modèles de régression.

L’objectif est double :

1. Réaliser une analyse exploratoire approfondie du dataset.
2. Appliquer différents modèles prédictifs (linéaire, polynomial, arbre de décision, forêt aléatoire, SVR) pour comparer leurs performances.

---

## 2. Importation des librairies

### Code (extrait)

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import PolynomialFeatures, StandardScaler
from sklearn.tree import DecisionTreeRegressor
from sklearn.ensemble import RandomForestRegressor
from sklearn.svm import SVR
from sklearn.metrics import mean_squared_error, r2_score
```

### Interprétation détaillée

Chaque bibliothèque importée joue un rôle clé dans la chaîne analytique :

* **pandas** permet la manipulation structurée du dataset Covid-19. Grâce à ses DataFrame, il devient possible de filtrer, fusionner, décrire et prétraiter les données.
* **numpy** est utilisé pour les opérations mathématiques rapides, indispensables pour créer des indices temporels, convertir des tableaux ou générer des transformations.
* **matplotlib.pyplot** assure la visualisation, essentielle pour comprendre l’évolution de la pandémie (tendances, pics, ruptures).
* **train_test_split** sépare les données en apprentissage et test afin de mesurer la capacité des modèles à généraliser.
* **LinearRegression, PolynomialFeatures** fournissent les outils de modélisation linéaire et polynomiale.
* **StandardScaler** rend possible la normalisation, indispensable pour les modèles sensibles à l’échelle comme le SVR.
* **DecisionTreeRegressor, RandomForestRegressor** permettent la modélisation non linéaire par arbres et ensembles.
* **SVR** capte les relations complexes grâce au noyau RBF.
* **mean_squared_error, r2_score** fournissent les métriques clés pour comparer objectivement les performances.

La combinaison de ces librairies constitue ainsi une boîte à outils complète allant de la préparation à la modélisation avancée.

---

## 3. Chargement du jeu de données

### Code (extrait)

```python
df = pd.read_csv('covid_data.csv')
```

### Interprétation détaillée

Le chargement du dataset constitue l’étape fondamentale, car la qualité et la structure des données influencent directement la pertinence des analyses. Les jeux de données Covid-19 contiennent généralement :

* des **dates** permettant de retracer l’évolution temporelle ;
* des **cas confirmés**, **décès** et **guérisons** ;
* parfois des taux de reproduction, hospitalisations ou indicateurs gouvernementaux.

Identifier la source (OMS, OurWorldInData, ministère de la santé…) est également important pour comprendre le niveau de précision et la fréquence des mises à jour. Cette étape prépare le terrain pour toutes les analyses ultérieures.

---

## 4. Analyse exploratoire du dataset

### Code (extrait)

```python
df.info()
df.describe()
df.isnull().sum()
```

### Interprétation détaillée

L’analyse exploratoire permet d’obtenir une vision globale et critique du dataset :

* `df.info()` révèle la taille, les types de variables et la présence de valeurs non numériques.
* `df.describe()` fournit des statistiques fondamentales (moyenne, médiane, minimum, maximum, écart‑type), permettant d’évaluer la dispersion typique des données épidémiologiques.
* `df.isnull().sum()` identifie les colonnes à problèmes. Dans les données Covid, les valeurs manquantes apparaissent souvent à cause de retards de communication, de sous‑déclaration ou de corrections administratives.

Cette phase est cruciale : un mauvais traitement des anomalies peut conduire à des modèles totalement biaisés.

---

## 5. Prétraitement et Feature Engineering

### Code (extrait)

```python
df = df.dropna()
df['day_index'] = np.arange(len(df))
X = df[['day_index']]
y = df['confirmed_cases']
```

### Interprétation détaillée

Le prétraitement consiste à rendre les données compatibles avec la modélisation :

* **Suppression des valeurs manquantes** : bien que simple, cette approche garantit des données propres, mais peut éliminer des journées critiques. Une alternative serait l’imputation.
* **Création de `day_index`** : transformer les dates en un index numérique permet aux modèles de machine learning de comprendre l’évolution sans manipuler directement des objets datetime.
* **Définition des variables X et y** : ici, l’objectif est de prédire les cas confirmés en fonction du temps. Ce choix est pertinent pour observer les dynamiques globales de la pandémie.

Cette étape forme la base de la modélisation et influence fortement la qualité des prédictions.

---

## 6. Analyse descriptive et visualisations

### Code (extrait)

```python
plt.plot(df['day_index'], df['confirmed_cases'])
plt.title('Évolution des cas confirmés')
plt.xlabel('Jours')
plt.ylabel('Cas confirmés')
plt.show()
```

### Interprétation détaillée

La visualisation constitue un outil indispensable avant la modélisation :

* La courbe permet d’observer immédiatement les **phases de croissance rapide**, les **pics**, les **plateaux** et les **décélérations**.
* Les épidémies présentent souvent une forme en **S** ou en **vagues**, avec des hausses exponentielles suivies de stabilisations.
* Cette observation guide le choix des modèles : les régressions simples seront insuffisantes, tandis que les modèles non linéaires seront mieux adaptés.

Une bonne visualisation oriente ainsi la méthodologie et met en évidence la complexité sous‑jacente des données Covid‑19.

---

## 7. Méthodologie de modélisation

### Rappel méthodologique

La démarche suivie respecte les bonnes pratiques de data science :

1. **Division du dataset en train et test** : permet de vérifier que le modèle généralise sur des données jamais vues, ce qui est crucial dans un contexte dynamique comme une pandémie.
2. **Application de plusieurs modèles** : chaque modèle capture une forme différente de relation (linéaire, polynomiale, segmentation, interactions complexes…).
3. **Comparaison via RMSE et R²** : ces métriques quantifient l’erreur et la qualité explicative. Elles permettent d’identifier le modèle le plus adapté.

### Interprétation détaillée

Cette méthodologie garantit une analyse robuste et complète. Tester plusieurs modèles est essentiel car aucune méthode unique ne suffit à caractériser l’évolution irrégulière et non stationnaire d’une pandémie. La combinaison d’indicateurs (RMSE, R²) offre une vision équilibrée entre précision et cohérence statistique. Cette approche est indispensable pour tirer des conclusions fiables.

---

## 8. Régression Linéaire — sur `day_index`

### Code (extrait)

```python
from sklearn.linear_model import LinearRegression
X_train = df[["day_index"]].values[:split_idx]
X_test  = df[["day_index"]].values[split_idx:]
model_lr = LinearRegression().fit(X_train, y_train)
pred_lr = model_lr.predict(X_test)

rmse_lr = np.sqrt(mean_squared_error(y_test, pred_lr))
r2_lr = r2_score(y_test, pred_lr)
```

### Résultats (synthétique)

* **RMSE = 41.52**
* **R² = -0.298**

### Interprétation détaillée

La régression linéaire constitue le modèle le plus simple : elle impose une relation strictement proportionnelle entre le temps (`day_index`) et les décès. Or, dans une pandémie, l’évolution est rarement linéaire : elle suit plutôt des phases exponentielles, des plateaux, puis des décroissances. Le modèle ne parvient donc pas à représenter ces ruptures de tendance. Le **R² négatif** indique que le modèle est moins performant qu’un prédicteur constant. Le RMSE relativement élevé traduit un écart important entre les valeurs prédites et observées. La linéarité est donc trop restrictive pour ce type de données.

### Recommandations

* Éviter d’utiliser la régression linéaire seule pour des séries épidémiologiques.
* Ajouter des transformations (logs, dérivées, moyennes mobiles).
* Opter pour des modèles capables de capter la non‑linéarité.

---

## 9. Régression Polynomiale (degré 2) — sur `cum_cases`

### Code (extrait)

```python
from sklearn.preprocessing import PolynomialFeatures
poly = PolynomialFeatures(degree=2, include_bias=False)
X_poly_train = poly.fit_transform(df[["cum_cases"]].values[:split_idx])
X_poly_test  = poly.transform(df[["cum_cases"]].values[split_idx:])
model_poly = LinearRegression().fit(X_poly_train, y_train)
pred_poly = model_poly.predict(X_poly_test)

rmse_poly = np.sqrt(mean_squared_error(y_test, pred_poly))
r2_poly = r2_score(y_test, pred_poly)
```

### Résultats (synthétique)

* **RMSE = 35.33**
* **R² = -0.1430**

### Interprétation détaillée

La régression polynomiale de degré 2 ajoute un terme quadratique à la variable explicative (`cum_cases`), ce qui lui permet de capturer une relation non linéaire douce. Cependant, dans le contexte de la pandémie Covid‑19, la dynamique de mortalité dépend de multiples facteurs : délais entre infection et décès, intensité de propagation, variations journalières, interventions publiques et bruit important dans les données.

Limiter le modèle à une seule variable cumulée rend la courbe quadratique insuffisante pour représenter fidèlement l’évolution réelle. Le **R² négatif** traduit une incapacité du modèle à expliquer la variance, faisant même pire qu'une simple moyenne. Le **RMSE relativement élevé** suggère une mauvaise spécification fonctionnelle et un potentiel **sur‑ajustement** dû à la forme quadratique qui ne correspond pas à la vraie relation.

### Recommandations

* Étendre les variables utilisées dans la transformation polynomiale (ex. : décès retardés, moyennes mobiles, taux de croissance).
* Appliquer une régularisation (Ridge ou Lasso) pour limiter la variance.
* Tester différents degrés via validation croisée afin d'éviter de sur‑adapter la courbe.

---

## 10. Arbre de Décision — sur `day_index`

### Code (extrait)

```python
from sklearn.tree import DecisionTreeRegressor
X_train = df[["day_index"]].values[:split_idx]
X_test  = df[["day_index"]].values[split_idx:]
dt = DecisionTreeRegressor(max_depth=5, random_state=0)
dt.fit(X_train, y_train)
pred_dt = dt.predict(X_test)

rmse_dt = np.sqrt(mean_squared_error(y_test, pred_dt))
r2_dt = r2_score(y_test, pred_dt)
```

### Résultats (synthétique)

* **RMSE = 18.90**
* **R² = 0.62**

### Interprétation détaillée

L’arbre de décision découpe la série temporelle en segments, apprenant des seuils qui créent des comportements locaux. Ce modèle capture bien les ruptures brusques dues aux vagues épidémiques, confinements, réouvertures ou pics soudains. Le **R² élevé** montre qu’il reproduit bien la structure des données. Cependant, les arbres ont une **forte variance** : ils peuvent apprendre trop fidèlement les irrégularités, surtout s’ils ne sont pas limités en profondeur. Le choix de `max_depth=5` atténue ce risque.

### Recommandations

* Augmenter légèrement la profondeur pour tester l’amélioration.
* Utiliser ce modèle comme base, mais privilégier des méthodes d’ensemble plus stables.
* Valider par cross-validation pour éviter le sur-apprentissage.

---

## 11. Forêt Aléatoire — sur `day_index`

### Code (extrait)

```python
from sklearn.ensemble import RandomForestRegressor
X_train = df[["day_index"]].values[:split_idx]
X_test  = df[["day_index"]].values[split_idx:]
rf = RandomForestRegressor(n_estimators=200, max_depth=8, random_state=0)
rf.fit(X_train, y_train)
pred_rf = rf.predict(X_test)

rmse_rf = np.sqrt(mean_squared_error(y_test, pred_rf))
r2_rf = r2_score(y_test, pred_rf)
```

### Résultats (synthétique)

* **RMSE = 14.11**
* **R² = 0.78**

### Interprétation détaillée

La Forêt Aléatoire réduit la variance des arbres individuels en agrégeant plusieurs modèles formés sur des sous-échantillons aléatoires. Elle capte les non‑linéarités, les ruptures et la diversité des comportements sans sur-apprendre le bruit. Le **RMSE le plus faible** et un **R² élevé** montrent que ce modèle s’adapte particulièrement bien aux données épidémiques. Sa robustesse le rend approprié pour des prévisions opérationnelles.

### Recommandations

* Tester l’augmentation du nombre d’arbres (`n_estimators`) pour stabiliser davantage.
* Inclure plusieurs features temporelles pour encore améliorer la précision.
* Utiliser ce modèle comme référence pour la comparaison finale.

---

## 12. Support Vector Regression (SVR) — noyau RBF

### Code (extrait)

```python
from sklearn.svm import SVR
from sklearn.preprocessing import StandardScaler
X_scaled_train = scaler.fit_transform(df[["day_index"]].values[:split_idx])
X_scaled_test  = scaler.transform(df[["day_index"]].values[split_idx:])
svr = SVR(kernel='rbf', C=10, gamma=0.1)
svr.fit(X_scaled_train, y_train)
pred_svr = svr.predict(X_scaled_test)

rmse_svr = np.sqrt(mean_squared_error(y_test, pred_svr))
r2_svr = r2_score(y_test, pred_svr)
```

### Résultats (synthétique)

* **RMSE = 16.70**
* **R² = 0.70**

### Interprétation détaillée

Le SVR à noyau RBF est l’un des modèles les plus puissants pour capturer des formes complexes grâce à son noyau non linéaire. Il apprend des fonctions lisses capables de reproduire l’évolution des décès sur plusieurs phases. Cependant, sa performance dépend fortement de l’échelle des données, des hyperparamètres (`C`, `gamma`) et du coût computationnel. Ici, son RMSE légèrement plus élevé que celui de la Forêt Aléatoire montre qu’il s’adapte bien, mais qu’un réglage plus fin pourrait améliorer encore les résultats.

### Recommandations

* Ajuster les hyperparamètres via GridSearch.
* Ajouter des variables dérivées pour enrichir la dynamique.
* Utiliser SVR comme modèle complémentaire en prévision courte.

---

## 13. Comparaison globale des modèles

```python
models = {
    'Régression Linéaire': y_pred_lr,
    'Régression Polynomiale': y_pred_poly[-len(y_test):],
    'Arbre de Décision': y_pred_dt,
    'Forêt Aléatoire': y_pred_rf,
    'SVR': y_pred_svr[-len(y_test):]
}

for name, pred in models.items():
    print(name, 'RMSE:', np.sqrt(mean_squared_error(y_test, pred)))
    print(name, 'R²:', r2_score(y_test, pred))
```

### Interprétation générale

En général :

* La régression linéaire est la moins performante.
* Le modèle polynomial est meilleur mais sensible au surapprentissage.
* L’arbre est précis mais instable.
* La forêt aléatoire offre souvent le meilleur compromis précision/stabilité.
* Le SVR est très performant mais plus lourd à entraîner.

---

## 14. Conclusion Générale

L’analyse de la pandémie Covid‑19 via différents modèles montre que les méthodes non linéaires sont les plus adaptées pour capturer la dynamique réelle d’une crise sanitaire. Les modèles ensembles comme la Forêt Aléatoire et les modèles à noyau comme le SVR se démarquent par leur capacité à représenter la complexité de l’évolution des cas.

Cette étude démontre l’importance du choix du modèle pour prévoir l’évolution d’une pandémie et appuyer la prise de décision publique.





























