
 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>   <img src="encg settat.png" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2









---

# COMPTE RENDU 

## Analyse du Dataset *Air Quality – Health Impact*

### Projet Data Science – Régression et Modélisation Prédictive

---

## Introduction Générale

La pollution de l’air est reconnue comme l’un des principaux facteurs de risque environnementaux pour la santé humaine. Les particules fines, les gaz polluants et les composés chimiques présents dans l’atmosphère ont des effets cumulatifs sur l’organisme, pouvant provoquer des maladies respiratoires, cardiovasculaires et neurologiques. Ces effets sont souvent progressifs et dépendent de la durée d’exposition ainsi que de la concentration des polluants.

L’évaluation de l’impact sanitaire de la qualité de l’air repose traditionnellement sur des méthodes statistiques classiques et des seuils réglementaires. Bien que ces approches soient utiles, elles présentent des limites lorsqu’il s’agit de capturer des **interactions complexes et non linéaires** entre plusieurs polluants agissant simultanément. Dans ce contexte, la **Data Science** et le **Machine Learning** constituent une alternative moderne, permettant d’exploiter un grand volume de données afin de **modéliser et prédire l’impact sanitaire** à partir de mesures environnementales objectives.
Contexte Métier et Problématique

---

# SOMMAIRE


**1. Contexte et Problématique**

**2. Présentation du Dataset**

**3. Simulation de Données Réalistes et Données Manquantes**

**4. Nettoyage des Données et Imputation**

**5. Analyse Exploratoire des Données (EDA)**

**6. Méthodologie de Modélisation**

**7. Évaluation des Performances**

**8. Analyse Graphique : Prédictions vs Réalité**

**9. Conclusion Générale**

---


## 1. Contexte et Problématique

### 1.1 Enjeu sanitaire et environnemental

La qualité de l’air dépend de nombreux facteurs, notamment les polluants atmosphériques, les conditions météorologiques et les activités humaines. Ces facteurs interagissent entre eux de manière complexe, ce qui rend l’évaluation de leur impact sur la santé difficile à analyser par des méthodes purement descriptives. Dans un contexte de prévention et de prise de décision publique, il est essentiel de disposer de **modèles prédictifs fiables** capables d’anticiper les risques sanitaires liés à la pollution atmosphérique et d’orienter les politiques environnementales.

### 1.2 Problématique du projet

La question centrale abordée dans ce projet est la suivante : **peut-on prédire l’impact sanitaire de la pollution de l’air à partir de mesures environnementales ?**
Une seconde question, d’ordre méthodologique, accompagne cette problématique : **un modèle de régression non linéaire est-il capable de capturer la complexité de la relation entre pollution atmosphérique et santé humaine ?**
Ces questions visent à évaluer à la fois la pertinence des données disponibles et la capacité du Machine Learning à modéliser un phénomène réel complexe.

---

## 2. Présentation du Dataset

Le dataset *Air Quality – Health Impact* regroupe des observations décrivant différentes **variables environnementales** liées à la qualité de l’air, associées à une **variable cible quantitative** représentant un indice global d’impact sanitaire. Les données sont majoritairement numériques et ne comportent pas de variables catégorielles, ce qui simplifie leur exploitation par des modèles de régression.

La relation entre les variables explicatives et la cible est potentiellement complexe et non linéaire, ce qui rend ce dataset particulièrement intéressant pour une approche de modélisation avancée. La nature **continue** de la variable cible justifie pleinement le recours à une **approche par régression**.

---

## 3. Simulation de Données Réalistes et Données Manquantes

### 3.1 Pourquoi introduire des valeurs manquantes ?

Dans des contextes réels de collecte de données environnementales, certaines mesures peuvent être absentes en raison de capteurs défectueux, de problèmes techniques ou d’erreurs humaines. Afin de reproduire ces conditions réalistes, une proportion de **5 % de valeurs manquantes** a été introduite artificiellement dans les variables numériques du dataset. Cette étape permet de tester la robustesse du pipeline de préparation des données.

### 3.2 Problématique des valeurs manquantes

Les algorithmes de Machine Learning ne peuvent pas fonctionner directement avec des valeurs manquantes (NaN). La présence de telles valeurs empêche l’entraînement du modèle et peut biaiser les résultats. Il est donc indispensable de procéder à un **nettoyage des données** avant toute phase de modélisation, afin d’assurer la cohérence et la qualité des données utilisées.

---

## 4. Nettoyage des Données et Imputation

### 4.1 Choix de la méthode d’imputation

Les valeurs manquantes ont été remplacées par la **moyenne de chaque variable**. Cette méthode est particulièrement adaptée lorsque le pourcentage de données manquantes est faible et que les variables sont continues. Elle permet de conserver l’ensemble des observations sans supprimer d’informations potentiellement utiles pour la modélisation.

### 4.2 Avantages et limites de l’imputation par la moyenne

L’imputation par la moyenne présente l’avantage d’être simple à mettre en œuvre et rapide, tout en maintenant la taille du dataset. Toutefois, elle peut entraîner une **réduction artificielle de la variance** et introduire un biais si les données ne sont pas manquantes de manière aléatoire. De plus, l’imputation ayant été réalisée avant la séparation des données en jeux d’entraînement et de test, un léger risque de **fuite d’information (data leakage)** peut exister dans un cadre professionnel.

---

## 5. Analyse Exploratoire des Données (EDA)

### 5.1 Objectifs de l’analyse exploratoire

L’analyse exploratoire des données a pour objectif de comprendre la structure du dataset, d’étudier la distribution des variables et d’identifier les relations entre les différentes features. Cette étape permet également de détecter d’éventuelles anomalies et d’évaluer la pertinence des variables explicatives vis-à-vis de la variable cible.

### 5.2 Résultats de l’EDA

Les statistiques descriptives révèlent des variables présentant des échelles et des dispersions différentes, ce qui reflète la diversité des phénomènes environnementaux mesurés. L’analyse des corrélations met en évidence des relations significatives entre certains polluants, ainsi qu’un lien clair entre plusieurs variables environnementales et l’impact sanitaire. Ces observations confirment que la qualité de l’air est un facteur déterminant pour la santé humaine.

---

## 6. Méthodologie de Modélisation

### 6.1 Séparation des données

Le dataset a été divisé en **80 % de données d’entraînement** et **20 % de données de test**. Cette séparation permet d’entraîner le modèle sur une partie des données et d’évaluer sa capacité de généralisation sur des observations jamais vues, ce qui est essentiel pour mesurer la performance réelle du modèle.

### 6.2 Choix du modèle

Le modèle retenu est un **RandomForestRegressor**, basé sur un ensemble d’arbres de décision. Ce choix est motivé par sa capacité à modéliser des **relations non linéaires**, sa robustesse face au bruit et sa bonne performance sur des phénomènes complexes tels que les données environnementales. De plus, ce type de modèle est peu sensible aux valeurs extrêmes et aux différences d’échelle entre les variables.

---

## 7. Évaluation des Performances

Les performances du modèle ont été évaluées à l’aide de trois métriques classiques de la régression : l’erreur quadratique moyenne (MSE), la racine de l’erreur quadratique moyenne (RMSE) et le coefficient de détermination (R²).

Tableau 1 : Résultats quantitatifs du modèle
| Métrique                       | Valeur obtenue | Interprétation                     |
| ------------------------------ | -------------- | ---------------------------------- |
| Mean Squared Error (MSE)       | **0.1701**     | Les erreurs importantes sont rares |
| Root Mean Squared Error (RMSE) | **0.4124**     | Erreur moyenne modérée             |
| R² Score                       | **0.6827**     | 68,27 % de la variance expliquée   |


Ces résultats montrent que le modèle parvient à expliquer une part importante de la variabilité de l’impact sanitaire, malgré la complexité intrinsèque du phénomène étudié.

Tableau 2 : Lecture qualitative des performances
| Indicateur        | Niveau        | Signification                           |
| ----------------- | ------------- | --------------------------------------- |
| Précision globale | Bonne         | Prédictions proches des valeurs réelles |
| Stabilité         | Élevée        | Peu de variations extrêmes              |
| Généralisation    | Satisfaisante | Pas de sur-apprentissage évident        |


---

## 8. Analyse Graphique : Prédictions vs Réalité

La visualisation des prédictions par rapport aux valeurs réelles montre une concentration des points autour de la diagonale idéale, indiquant une bonne adéquation entre les valeurs prédites et observées. La dispersion modérée observée suggère que certaines variations de l’impact sanitaire ne sont pas entièrement capturées par les variables disponibles, ce qui est cohérent avec la nature multifactorielle de la santé humaine. L’absence d’erreurs extrêmes indique que le modèle est stable et ne présente pas de sur-apprentissage marqué.

---

## 9. Conclusion Générale

Ce projet met en évidence l’apport important de la Data Science dans l’analyse de problématiques environnementales et sanitaires complexes. Les résultats obtenus montrent qu’il est possible de prédire l’impact sanitaire de la qualité de l’air à partir de données environnementales, avec un niveau de performance satisfaisant. Le modèle RandomForestRegressor parvient à expliquer une part significative de la variabilité de la variable cible, tout en maintenant des erreurs de prédiction modérées, ce qui confirme la pertinence de l’approche adoptée.

Malgré ces résultats encourageants, certaines limites doivent être soulignées. L’imputation des valeurs manquantes par la moyenne constitue une méthode simplifiée qui peut introduire un biais dans l’analyse. De plus, l’absence de validation croisée limite l’évaluation de la robustesse et de la capacité de généralisation du modèle. Par ailleurs, l’impact sanitaire dépend de nombreux facteurs non pris en compte dans le dataset, tels que les caractéristiques démographiques, socio-économiques ou environnementales.

Des améliorations futures peuvent être envisagées afin de renforcer la qualité du modèle. L’utilisation de méthodes d’imputation plus avancées, la mise en place d’une validation croisée, la comparaison avec d’autres modèles de régression et l’intégration de nouvelles variables explicatives permettraient d’améliorer les performances. À terme, ce type de modèle pourrait constituer un outil d’aide à la décision en santé publique pour anticiper et prévenir les risques sanitaires liés à la pollution atmosphérique.

---

