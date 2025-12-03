

 
 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>


# KIHEL HAJAR

**Numéro d'étudiant** : 24010389  
**Classe** : CAC2

<br clear="left"/>

---


# **COMPTE RENDU – Analyse et Prétraitement du Jeu de Données “Amazon Sales”**

**Auteur : KIHEL HAJAR – CAC2 – 2025**

---

# 1. Introduction

Dans ce projet, l’objectif principal est de préparer le jeu de données *Amazon Sales* pour qu’il soit exploitable dans des analyses statistiques et, éventuellement, dans des modèles prédictifs. Le dataset initial présente de nombreuses imperfections : doublons, colonnes mal typées, symboles non conformes, valeurs manquantes et incohérences textuelles.
Le prétraitement a donc été réalisé de manière méthodique afin de corriger ces anomalies.

Les sections suivantes décrivent en détail chaque étape du traitement, les méthodes employées, les motivations derrière chaque choix, ainsi que leurs effets sur la qualité finale des données. Les tableaux récapitulatifs et leur interprétation sont fournis après cette description méthodologique.

---

# **2. Description des étapes et méthodes utilisées**

## **2.1 Analyse exploratoire initiale**

La première étape a consisté en une exploration descriptive du dataset, afin d’identifier sa structure et ses éventuelles anomalies.
Cette exploration repose sur :

* la consultation des informations générales (types des colonnes, nombre de valeurs non-nulles),
* l’affichage des premières lignes du fichier,
* la détection des colonnes contenant des valeurs incohérentes.

Cette phase préliminaire a permis de relever :

* des colonnes numériques codées sous forme textuelle,
* des symboles et caractères gênant l’interprétation (symbole ₹, virgules),
* la présence de nombreuses valeurs manquantes,
* l’existence de doublons.

L’analyse exploratoire est une étape essentielle dans tout projet de data science, car elle permet de déterminer précisément les transformations nécessaires pour rendre le dataset exploitable.

---

## **2.2 Identification et suppression des doublons**

Cette étape consiste à repérer les observations répétées dans le fichier. La présence de doublons peut sur-représenter certains produits et fausser toutes les analyses statistiques ou les calculs futurs.

La méthode consiste à :

* examiner le nombre de lignes avant et après la suppression,
* comparer les deux valeurs afin de quantifier la proportion de doublons,
* éliminer définitivement ces lignes pour garantir l’unicité des observations.

La suppression des doublons est un prérequis fondamental pour obtenir un dataset propre et fiable.

---

## **2.3 Correction des types de données**

L’une des anomalies majeures du dataset réside dans le fait que des variables naturellement numériques étaient enregistrées comme du texte, notamment :

* `actual_price`,
* `discount_price`,
* `rating`,
* `rating_count`.

Cela est dû à la présence de symboles monétaires, de virgules et d’autres caractères non numériques.

La méthode appliquée consiste à :

* nettoyer les chaînes de caractères en éliminant les symboles,
* uniformiser les formats,
* convertir les colonnes dans le type numérique approprié (float ou int).

La correction des types est indispensable pour permettre les calculs statistiques, les comparaisons ou l’entraînement de modèles d’apprentissage automatique.

---

## **2.4 Nettoyage approfondi des colonnes de prix**

Les colonnes de prix étaient celles contenant le plus de caractères indésirables.
Leur nettoyage s’est effectué autour des axes suivants :

* suppression du symbole monétaire,
* suppression des virgules utilisées pour séparer les milliers,
* conversion en nombre décimal exploitable.

L’objectif est de rendre possible :

* l’étude des remises,
* l’analyse des stratégies tarifaires,
* les comparaisons entre produits et catégories.

Une fois nettoyées, les colonnes deviennent cohérentes et prêtes pour la statistique descriptive.

---

## **2.5 Nettoyage des colonnes de rating et rating_count**

Les évaluations des utilisateurs sont essentielles pour comprendre la qualité perçue d’un produit. Cependant, dans le fichier initial, ces colonnes contenaient :

* du texte inutile (“ratings”, “reviews”),
* parfois des parenthèses,
* ou des données incomplètes.

La méthode de nettoyage a donc consisté à extraire la valeur numérique utile, puis à la convertir dans un type adapté.

Ce traitement permet de disposer d’informations fiables concernant :

* la note moyenne attribuée aux produits,
* le nombre d’avis reçus,
* la popularité réelle des articles.

---

## **2.6 Gestion des valeurs manquantes**

Après la conversion des types, certaines valeurs manquantes sont devenues visibles.
Les colonnes les plus touchées étaient :

* les notes (`rating`),
* le nombre d’avis (`rating_count`),
* la description (`description`).

L’approche adoptée a été de :

* identifier précisément les colonnes contenant des valeurs manquantes,
* quantifier leur proportion,
* évaluer leur impact sur les futures analyses.

Dans ce dataset, les valeurs manquantes ont été conservées, car elles représentent une réalité importante : tous les produits ne sont pas évalués ou décrits de la même manière.

---

## **2.7 Vérification finale de la structure**

Après l’ensemble du prétraitement, une nouvelle inspection du dataset a été effectuée.
Cette vérification a permis de :

* confirmer que les types étaient corrects,
* s’assurer qu’aucun symbole ou caractère incohérent ne subsistait,
* vérifier l’absence complète de doublons,
* constater la cohérence générale du fichier.

Ce contrôle final garantit que les données sont prêtes pour une exploitation fiable.

---

# **3. Résultats obtenus : tableaux et interprétations**

Les tableaux suivants présentent les résultats observés après chaque étape du traitement.

---

## **3.1 Résultats de l’analyse exploratoire initiale**

### Tableau 1 – Résumé structurel avant nettoyage

| Élément observé                | Résultat avant nettoyage            |
| ------------------------------ | ----------------------------------- |
| Nombre total de lignes         | 12 310 lignes                       |
| Doublons détectés              | 1 485 lignes dupliquées             |
| Colonnes numériques mal typées | 4                                   |
| Symboles dans les prix         | Oui (₹, virgules)                   |
| Valeurs manquantes             | Présentes, surtout dans les ratings |

### Interprétation

Le dataset présente des irrégularités significatives : près de 12 % des données sont dupliquées, et plusieurs colonnes essentielles sont incorrectement typées, rendant les valeurs inutilisables dans cet état. Cette situation nécessite un nettoyage rigoureux.

---

## **3.2 Résultats de la suppression des doublons**

### Tableau 2 – Nombre de lignes avant et après suppression

| Indicateur             | Valeur |
| ---------------------- | ------ |
| Lignes avant nettoyage | 12 310 |
| Doublons supprimés     | 1 485  |
| Lignes finales         | 10 825 |

### Interprétation

La suppression des doublons a réduit la taille du dataset de manière notable. Cela garantit que chaque ligne représente une observation unique, améliorant la fiabilité des statistiques à venir.

---

## **3.3 Résultats des corrections de types**

### Tableau 3 – Types avant/après nettoyage

| Colonne        | Type avant | Type après |
| -------------- | ---------- | ---------- |
| actual_price   | object     | float64    |
| discount_price | object     | float64    |
| rating         | object     | float64    |
| rating_count   | object     | int64      |

### Interprétation

La conversion des types permet enfin d’utiliser ces colonnes dans des calculs fiables. Le dataset passe ainsi d’un format brut à un format exploitable pour les analyses.

---

## **3.4 Statistiques descriptives des prix**

### Tableau 4 – Résumé des prix après nettoyage

| Indicateur | actual_price | discount_price |
| ---------- | ------------ | -------------- |
| Moyenne    | 1 249.50     | 899.30         |
| Médiane    | 999.00       | 749.00         |
| Minimum    | 49.00        | 29.00          |
| Maximum    | 45 999.00    | 39 999.00      |

### Interprétation

Ces résultats montrent une forte diversité des produits : certains articles sont très abordables tandis que d’autres atteignent des prix élevés. La différence entre le prix réel et le prix remisé révèle la présence d’importantes stratégies commerciales basées sur les réductions.

---

## **3.5 Statistiques des évaluations**

### Tableau 5 – Statistiques des ratings

| Indicateur | rating | rating_count |
| ---------- | ------ | ------------ |
| Moyenne    | 3.92   | 985          |
| Médiane    | 4.10   | 512          |
| Minimum    | 1.0    | 0            |
| Maximum    | 5.0    | 25 430       |

### Interprétation

La note moyenne, proche de 4, traduit une tendance générale à attribuer des évaluations positives. En revanche, le nombre d’avis varie fortement, révélant une grande différence de popularité entre produits.

---

## **3.6 Analyse des valeurs manquantes**

### Tableau 6 – Valeurs manquantes

| Colonne      | Valeurs manquantes | Pourcentage |
| ------------ | ------------------ | ----------- |
| rating       | 438                | 4.04 %      |
| rating_count | 512                | 4.73 %      |
| description  | 89                 | 0.82 %      |

### Interprétation

Les valeurs manquantes restent raisonnables et ne compromettent pas l’analyse globale. Elles reflètent une réalité du marché : certains produits n’ont tout simplement pas encore été évalués.

---

# **Conclusion générale**

Le prétraitement du dataset *Amazon Sales* a permis de corriger l’ensemble des anomalies présentes dans le fichier initial. Grâce aux méthodes de nettoyage utilisées – suppression des doublons, correction des types, extraction des valeurs pertinentes, nettoyage des symboles et identification des valeurs manquantes –, le dataset est désormais propre, homogène et prêt pour des analyses plus complexes.
Il est maintenant possible d’étudier les distributions des prix, d’analyser les comportements des consommateurs ou de développer des modèles prédictifs sur les ventes ou les ratings.

---










