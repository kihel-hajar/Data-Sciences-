 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Prétraitement et Étude du Dataset Amazon Sales**

**Date :** 10 Décembre 2025
**Auteur :** KIHEL HAJAR
Voici **une version complète, réécrite et adaptée exactement au style du document “Correction Projet.md”**, mais appliquée **à votre projet Linnerud**, avec **ajout d’une problématique**, une structure pédagogique, des explications profondes, et vos vrais résultats.

Aucun emoji utilisé, même style analytique, même profondeur technique.

---

# GUIDE COMPLET : ANATOMIE DU PROJET LINNERUD


---

# **1. Le Contexte Métier et la Mission**

## **Le Problème (Problématique du Projet)**

L’analyse de la condition physique repose souvent sur plusieurs indicateurs mesurés séparément. Cependant, ces mesures ne sont pas toujours simples à interpréter et peuvent dépendre de plusieurs facteurs physiologiques.
Dans un cadre sportif ou médical, il serait utile de pouvoir **prédire automatiquement le niveau de performance global d’un individu** à partir de quelques tests simples.

**Problématique :**
À partir de trois mesures physiques (tractions, sit-ups, sauts), peut-on construire un modèle capable de **classifier automatiquement un individu selon son niveau de performance**, afin d’aider coaches ou professionnels de santé dans l’évaluation physique ?

## **Les Données (L’Input)**

Nous utilisons le **Linnerud Physical Exercise Dataset**.
Il contient trois mesures quantitatives :

* Chins (nombre de tractions)
* Sit-ups (nombre d’abdominaux)
* Jumps (hauteur du saut vertical)

Comme aucune variable cible n’existe, nous créons une cible binaire à partir de la variable *Chins* :

* 0 : performance inférieure ou égale à la médiane
* 1 : performance supérieure à la médiane

Cette cible est une abstraction pédagogique permettant de transformer un problème de régression en problème de classification.

---

# **2. Le Code Python (Laboratoire)**

Le script met en œuvre toutes les étapes du cycle de vie d’un projet Data Science :

1. Chargement des données
2. Simulation de données manquantes
3. Nettoyage et imputation
4. Analyse exploratoire
5. Split Train/Test
6. Entraînement d’un Random Forest
7. Évaluation des performances

Cette structure permet de reproduire un pipeline réaliste.

---

# **3. Analyse Approfondie : Nettoyage (Data Wrangling)**

## **La Nature du Problème des Données Manquantes**

Les algorithmes de Machine Learning ne tolèrent pas les valeurs `NaN`.
Une seule valeur manquante peut empêcher la construction de l’espace de distance entre individus.

Dans ce projet, 5 % de valeurs manquantes ont été ajoutées artificiellement pour simuler une situation réaliste.

## **Méthode d’imputation utilisée**

`SimpleImputer(strategy='mean')` remplace chaque valeur manquante par la moyenne de sa colonne.

Mécanisme en deux étapes :

1. **Fit :** la moyenne est calculée pour chaque variable.
2. **Transform :** les trous sont remplis par cette moyenne.

Ce choix est cohérent avec des données numériques continues et une faible proportion de valeurs manquantes.

---

# **4. Analyse Approfondie : Exploration (EDA)**

## **Statistiques descriptives**

Les variables Chins, Sit-ups et Jumps présentent une dispersion cohérente avec des mesures physiques.
Aucune distribution n’est fortement asymétrique, ce qui rend l’imputation par la moyenne raisonnable.

## **Corrélation entre variables**

La matrice de corrélation montre des liens positifs entre les variables :

* Un individu performant sur un exercice tend à l’être sur les autres.

Cette structure reflète un bon niveau de condition physique générale.

Le Random Forest n’est pas sensible à la multicorrélation, ce qui en fait un choix adéquat ici.

---

# **5. Analyse Approfondie : Méthodologie (Split)**

Le split 80/20 permet :

* d’entraîner le modèle sur 80 % des données,
* d’évaluer la capacité de généralisation sur les 20 % restants.

Cependant, avec un dataset aussi réduit (20 individus), le jeu de test ne contient que 4 individus, ce qui rend l’évaluation très instable.
Une seule erreur modifie fortement l’accuracy.

---

# **6. Focus Théorique : L’Algorithme Random Forest**

Le Random Forest est un ensemble d’arbres décisionnels utilisant :

* le bootstrap (échantillons aléatoires)
* un sous-ensemble de variables à chaque split

Ces mécanismes créent des arbres diversifiés dont les erreurs se compensent.
Le vote final fournit une prédiction robuste, même si chaque arbre individuel est fragile.

Ce comportement est adapté aux petits datasets, mais la très faible taille du jeu de test rend l’évaluation bruitée.

---

# **7. Analyse Approfondie : Évaluation des Résultats**

Voici les résultats chiffrés obtenus :

### **7.1 Accuracy globale**

**Accuracy = 50 %**

Le modèle ne prédit correctement qu’un individu sur deux.
Ce résultat est insuffisant pour un modèle opérationnel, mais explicable par :

* la taille très réduite du jeu de test,
* la cible artificielle,
* la variabilité naturelle du dataset.

---

### **7.2 Rapport de classification**

| Classe | Précision | Rappel | F1-score | Support |
| ------ | --------- | ------ | -------- | ------- |
| 0      | 1.00      | 0.33   | 0.50     | 3       |
| 1      | 0.33      | 1.00   | 0.50     | 1       |

**Analyse :**

* Pour la classe 0, le modèle identifie parfaitement les prédictions qu’il ose faire (précision = 1.00) mais manque la majorité des individus (rappel = 0.33).
* Pour la classe 1, le modèle détecte tous les vrais cas (rappel = 1.00) mais se trompe fréquemment lorsqu’il prédit cette classe (précision = 0.33).

Cela signifie que le modèle montre une **forte instabilité** dans la séparation des classes.

---

### **7.3 Matrice de confusion**

| Réel / Prédit | 0 | 1 |
| ------------- | - | - |
| Classe 0      | 1 | 2 |
| Classe 1      | 0 | 1 |

Interprétation :

* Deux individus réellement de classe 0 sont classés en classe 1.
* Aucun individu de classe 1 n’est mal classé.
* Le modèle a tendance à privilégier la prédiction de la classe 1.

---

# **8. Conclusion du Projet**

Ce projet illustre les étapes essentielles du cycle de vie d’un modèle machine learning.
Cependant, les résultats montrent que le modèle ne peut pas être considéré comme fiable dans les conditions actuelles.

Les principales limites sont :

1. La taille extrêmement réduite du dataset.
2. La cible artificielle créée à partir d’une médiane.
3. La très faible taille du jeu de test (4 individus seulement).
4. La difficulté de généralisation sur des données aussi peu nombreuses.

Pour aller plus loin, il serait nécessaire :

* d’utiliser un dataset plus large,
* d’appliquer une validation croisée,
* d’envisager des méthodes adaptées aux petits échantillons,
* de travailler sur une cible mieux définie.

Ce projet reste néanmoins une bonne démonstration pédagogique des concepts clés :
préparation, visualisation, modélisation, évaluation et interprétation.

---





