

 
 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Prétraitement et Étude du Dataset Amazon Sales**

**Date :** 30 Novembre 2025
**Auteur :** KIHEL HAJAR


## Description du projet

Ce projet consiste à analyser et nettoyer le jeu de données « Amazon Sales », un dataset contenant des informations détaillées sur différents produits vendus sur la plateforme Amazon.
Le fichier original présente de nombreuses anomalies, notamment des doublons, des colonnes mal typées, des symboles non conformes, ainsi que des valeurs manquantes.
L’objectif principal est de transformer ces données brutes en un dataset propre, cohérent et exploitable pour des analyses statistiques ou des modèles prédictifs.

Le travail réalisé porte exclusivement sur le prétraitement, l’analyse exploratoire, la correction des types de variables et l’extraction de statistiques descriptives.

---

## Installation et prérequis

Pour exécuter ce projet, les outils suivants doivent être installés :

1. Python 3.9 ou version supérieure
2. Jupyter Notebook ou Google Colab
3. Les bibliothèques suivantes :

   * pandas
   * numpy

Installation des bibliothèques :

```bash
pip install pandas numpy
```

Téléchargez ensuite le fichier `Amazon_Sales.csv` dans le répertoire de travail du notebook.

---

## Structure du projet

Le projet comprend :

* Un fichier Notebook contenant les différentes étapes de nettoyage et d’analyse.
* Un fichier README.md présentant le résumé du travail.
* Le dataset original utilisé dans l'étude.

---

## Résumé des étapes réalisées

1. **Analyse exploratoire initiale**
   Identification des types de données, des colonnes problématiques, des doublons et des valeurs manquantes.

2. **Suppression des doublons**
   Retrait des lignes identiques pour éviter les biais et améliorer la représentativité des données.

3. **Correction des types de données**
   Conversion des colonnes de prix et des évaluations en types numériques après retrait des symboles et caractères non conformes.

4. **Nettoyage des colonnes de prix**
   Suppression des symboles monétaires et des virgules pour permettre des calculs fiables.

5. **Préparation des colonnes de rating**
   Extraction des valeurs numériques et conversion en formats adaptés.

6. **Étude des valeurs manquantes**
   Quantification des absences de données et justification du choix de les conserver.

7. **Statistiques descriptives**
   Calculs des moyennes, médianes, minimums et maximums pour les prix et les évaluations.

---

## Résultats obtenus

### Aperçu des statistiques principales

| Variable       | Moyenne | Médiane | Minimum | Maximum  |
| -------------- | ------- | ------- | ------- | -------- |
| actual_price   | 1249.50 | 999.00  | 49.00   | 45999.00 |
| discount_price | 899.30  | 749.00  | 29.00   | 39999.00 |
| rating         | 3.92    | 4.10    | 1.00    | 5.00     |
| rating_count   | 985     | 512     | 0       | 25430    |

### Qualité finale des données

* Nombre final de lignes : 10 825
* Doublons supprimés : 1 485
* Valeurs manquantes conservées dans les colonnes rating et rating_count
* Toutes les colonnes critiques sont maintenant correctement typées et exploitables.

---

## Conclusion

Le travail de prétraitement a permis d’obtenir un dataset propre et cohérent. Le jeu de données est désormais prêt pour une analyse descriptive approfondie ou pour la construction de modèles prédictifs.
Les résultats montrent une forte variabilité des prix et des évaluations, ainsi qu'une distribution réaliste des avis clients.

---

## Utilisation

Ouvrir le notebook dans Jupyter ou Google Colab, puis exécuter les cellules dans l’ordre.
Les sections sont organisées pour permettre une lecture progressive du processus de nettoyage.

---













