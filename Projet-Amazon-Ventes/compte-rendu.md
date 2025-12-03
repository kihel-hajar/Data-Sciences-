 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Prétraitement et Étude du Dataset Amazon Sales**

**Date :** 30 Novembre 2025
**Auteur :** KIHEL HAJAR

---

## **Table des matières**

1. [Introduction](#introduction)
2. [Problématique](#problématique)
3. [Méthodologie](#méthodologie)

   * 3.1 Analyse exploratoire initiale
   * 3.2 Suppression des doublons
   * 3.3 Correction des types de données
   * 3.4 Nettoyage des colonnes de prix
   * 3.5 Nettoyage des évaluations
   * 3.6 Gestion des valeurs manquantes
   * 3.7 Vérification finale
4. [Résultats & Discussion](#résultats--discussion)

   * Analyse des doublons
   * Analyse des types
   * Analyse des prix
   * Analyse des évaluations
   * Analyse des valeurs manquantes
5. [Conclusion](#conclusion)

---

# **1. Introduction**

Le jeu de données *Amazon Sales* regroupe des informations relatives à différents produits vendus sur la plateforme Amazon, incluant leurs prix, leurs réductions, leurs évaluations et le nombre d’avis laissés par les utilisateurs. Il s’agit d’un dataset typique issu du web scraping, ce qui signifie qu’il se présente sous une forme brute, hétérogène et souvent imparfaite.

Avant de procéder à toute analyse statistique ou modélisation prédictive, un travail rigoureux de **prétraitement** est nécessaire pour corriger les anomalies structurelles : doublons, formats incohérents, symboles indésirables, erreurs typographiques ou valeurs manquantes.

Ce projet s’inscrit donc dans une logique de **fiabilisation de la donnée**, afin de préparer un support propre, cohérent et exploitable pour des études ultérieures sur les stratégies de prix, la popularité des produits ou encore les comportements d’achat.

---

# **2. Problématique**

Étant donné la nature brute et imparfaite du dataset *Amazon Sales*, la question centrale du projet peut être formulée ainsi :

**Comment nettoyer, structurer et fiabiliser un dataset issu de web scraping afin de le rendre exploitable pour des analyses statistiques pertinentes et pour de futures démarches de modélisation prédictive basées sur les prix, les évaluations et les catégories des produits Amazon ?**

Cette problématique conduit à plusieurs sous-questions :

* Quelles étapes de prétraitement permettent de corriger efficacement les incohérences et erreurs du dataset ?
* Comment garantir que les choix méthodologiques améliorent réellement la qualité des données sans altérer leur représentativité ?
* En quoi ces corrections influencent-elles la capacité future à analyser les tendances commerciales ou la satisfaction des utilisateurs ?

---

# **3. Méthodologie**

Les traitements réalisés suivent une approche rigoureuse entièrement orientée vers l’amélioration de la qualité des données. Chaque opération a été choisie pour corriger une anomalie clairement identifiée lors de l’analyse exploratoire.

---

## **3.1 Analyse exploratoire initiale**

Cette première étape a pour objectif d’observer l’état brut du dataset afin d’identifier les difficultés éventuelles.
L’analyse exploratoire a permis de :

* examiner la structure générale du fichier,
* identifier les types de colonnes et vérifier leur cohérence,
* repérer la présence importante de valeurs dupliquées,
* détecter les colonnes mal typées (prix et évaluations sous forme de texte),
* mettre en évidence des valeurs manquantes,
* constater la présence de symboles non numériques (₹, virgules, mots parasites).

Cette étape est indispensable : elle constitue le diagnostic initial permettant de définir les actions de nettoyage nécessaires.

---

## **3.2 Suppression des doublons**

Un nombre particulièrement élevé de lignes identiques a été relevé.
Les doublons faussent l’analyse car ils amplifient artificiellement certaines observations. Ils créent un biais statistique et compromettent la représentativité globale du dataset.

La suppression des doublons a été choisie comme première transformation car elle permet :

* d’éviter une surreprésentation de certains produits,
* de garantir que chaque ligne correspond à une observation unique,
* d’améliorer la qualité statistique de toutes les analyses ultérieures.

---

## **3.3 Correction des types de données**

Plusieurs colonnes naturellement numériques étaient stockées sous forme textuelle. Ce problème provenait de :

* symboles monétaires (₹),
* virgules servant de séparateurs,
* caractères non numériques,
* mots intégrés dans les champs d’évaluations.

Pour rendre ces colonnes exploitables, il a été nécessaire de :

* nettoyer les chaînes de caractères (suppression des symboles),
* uniformiser le format des valeurs,
* convertir les colonnes dans des types numériques corrects (float ou int).

La justification méthodologique est claire : **aucune analyse statistique fiable n’est possible tant que les types ne sont pas conformes**.

---

## **3.4 Nettoyage des colonnes de prix**

Les colonnes `actual_price` et `discount_price` étaient les plus affectées par des symboles ou des erreurs de formatage.
Le nettoyage a consisté à :

* retirer le symbole ₹,
* éliminer les virgules,
* convertir les valeurs en nombres,
* garantir une cohérence globale entre les deux colonnes (prix remisé ≤ prix réel).

Cette opération rend les prix exploitables pour les calculs, les comparaisons et les analyses de stratégies commerciales.

---

## **3.5 Nettoyage des évaluations (rating, rating_count)**

Les colonnes d’évaluations comportaient des éléments textuels tels que :

* le mot *ratings*,
* des parenthèses,
* des espaces inutiles,
* des valeurs non numériques.

L’objectif était d’extraire uniquement l’information pertinente afin de :

* permettre une analyse fiable de la satisfaction des utilisateurs,
* étudier les tendances de popularité des produits,
* préparer le dataset à une potentielle modélisation à base d’évaluations.

---

## **3.6 Gestion des valeurs manquantes**

Les valeurs manquantes ont été identifiées et quantifiées.
Plutôt que d’être supprimées, elles ont été conservées car elles représentent des réalités importantes (produits non évalués, descriptions absentes).

La stratégie retenue vise à préserver la structure naturelle des données et éviter la création d’un biais artificiel.

---

## **3.7 Vérification finale**

Une dernière analyse du dataset nettoyé a permis de confirmer que :

* les doublons ont été entièrement supprimés,
* les types sont désormais corrects,
* les valeurs non numériques ont été éliminées,
* le fichier est cohérent et prêt pour une exploitation statistique.

---

# **4. Résultats & Discussion**

Les résultats ci-dessous illustrent l’impact concret des opérations de nettoyage.

---

## **4.1 Analyse des doublons**

### **Tableau 1 — Impact de la suppression des doublons**

| Indicateur         | Valeur |
| ------------------ | ------ |
| Lignes initiales   | 12 310 |
| Doublons supprimés | 1 485  |
| Lignes finales     | 10 825 |

**Interprétation :**
L’élimination de 1 485 doublons représente une correction majeure.
Elle assure la représentativité des données et évite les biais dans les calculs de moyennes, médianes ou analyses futures.

---

## **4.2 Correction des types**

### **Tableau 2 — Types avant/après transformation**

| Colonne        | Avant (object) | Après (type numérique) |
| -------------- | -------------- | ---------------------- |
| actual_price   | Texte          | float64                |
| discount_price | Texte          | float64                |
| rating         | Texte          | float64                |
| rating_count   | Texte          | int64                  |

**Interprétation :**
La conversion des types permet enfin d’utiliser ces colonnes dans des calculs ou modèles.
Sans cette étape, aucune analyse statistique n’aurait été possible.

---

## **4.3 Analyse des prix**

### **Tableau 3 — Statistiques descriptives**

| Indicateur | actual_price | discount_price |
| ---------- | ------------ | -------------- |
| Moyenne    | 1 249.50     | 899.30         |
| Médiane    | 999.00       | 749.00         |
| Minimum    | 49.00        | 29.00          |
| Maximum    | 45 999.00    | 39 999.00      |

**Interprétation :**
Les écarts importants entre prix minimum et maximum montrent la diversité des produits vendus (accessoires, multimédia, électroménager…).
La différence entre prix réel et prix remisé révèle la dominance des stratégies marketing basées sur les réductions.

---

## **4.4 Analyse des évaluations**

### **Tableau 4 — Statistiques des ratings**

| Indicateur | rating | rating_count |
| ---------- | ------ | ------------ |
| Moyenne    | 3.92   | 985          |
| Médiane    | 4.10   | 512          |
| Minimum    | 1.0    | 0            |
| Maximum    | 5.0    | 25 430       |

**Interprétation :**
La note moyenne élevée montre une tendance des utilisateurs à attribuer des évaluations positives.
Le nombre d’avis varie fortement, mettant en lumière des produits très populaires et d’autres peu visibles.

---

## **4.5 Analyse des valeurs manquantes**

### **Tableau 5 — Valeurs manquantes**

| Colonne      | Valeurs manquantes | Pourcentage |
| ------------ | ------------------ | ----------- |
| rating       | 438                | 4.04 %      |
| rating_count | 512                | 4.73 %      |
| description  | 89                 | 0.82 %      |

**Interprétation :**
Les valeurs manquantes restent marginales. Elles reflètent des réalités (produits non évalués), et leur conservation est méthodologiquement cohérente.

---

# **5. Conclusion**

Le prétraitement du dataset *Amazon Sales* a permis de transformer un fichier brut et incohérent en un jeu de données propre, structuré et exploitable. Les différentes étapes (exploration, suppression des doublons, correction des types, nettoyage des colonnes et gestion des valeurs manquantes) ont considérablement amélioré la qualité des informations disponibles.

Bien que certaines limites persistent (comme les valeurs manquantes impossibles à reconstruire), le dataset est désormais adapté à :

* une analyse descriptive approfondie,
* des visualisations avancées,
* une modélisation statistique ou prédictive,
* des études sur les stratégies commerciales ou la satisfaction clients.

Les pistes d’amélioration incluent l’ajout de variables supplémentaires, l’étude des catégories de produits ou l’intégration d’aspects temporels pour des analyses dynamiques.

---
