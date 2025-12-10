 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Prétraitement et Étude du Dataset Amazon Sales**

**Date :** 10 Décembre 2025
**Auteur :** KIHEL HAJAR


---

# **COMPTE RENDU – ANALYSE COMPLÈTE DU PROJET LINNERUD**

## **1. Contexte et Objectif du Projet**

Le jeu de données **Linnerud** contient trois mesures physiologiques liées à la performance sportive :

* Chins (tractions),
* Sit-ups (abdominaux),
* Jumps (sauts debout).

Comme le dataset ne fournit pas de variable cible, une cible binaire a été créée à partir de la variable **Chins**.
La médiane a été utilisée pour séparer les individus en deux catégories :

* Classe 0 : niveau faible ou moyen en tractions
* Classe 1 : niveau élevé en tractions

L’objectif du projet est de construire un modèle capable de **prédire l’appartenance à l’une de ces deux classes** en se basant sur les trois variables physiologiques.

---

## **2. Constitution et Préparation du Jeu de Données**

### **2.1 Simulation de données manquantes**

Pour reproduire les imperfections réelles d’un environnement industriel, 5 % de valeurs manquantes ont été injectées dans chaque variable.
Sur un dataset aussi petit (20 sujets), cette manipulation modifie légèrement la distribution des données, ce qui crée une situation plus réaliste pour évaluer la robustesse du modèle.

### **2.2 Nettoyage par imputation**

Une imputation par la moyenne a été appliquée.
Cette méthode est adaptée lorsque :

* les variables sont continues,
* les distributions sont relativement symétriques,
* la proportion de données manquantes est faible.

Après traitement, aucune valeur manquante ne subsiste, et les données sont exploitables par les algorithmes de classification.

---

## **3. Analyse Exploratoire des Données**

### **3.1 Statistiques descriptives**

Les trois variables présentent :

* une dispersion modérée,
* des valeurs dans des plages cohérentes pour des mesures physiques,
* une absence d’outliers extrêmes après imputation.

Cette stabilité statistique est favorable à l’entraînement d’un modèle, bien que la taille du dataset limite fortement la représentativité.

### **3.2 Relations entre les variables**

La matrice de corrélation montre des liens positifs entre les trois exercices :
un individu ayant de bonnes performances en tractions tend également à bien performer en sit-ups et en sauts.

Ce phénomène est logique sur le plan physiologique : il reflète une condition physique générale.

---

## **4. Méthodologie d’Entraînement**

Une séparation Train/Test de 80/20 a été réalisée.

* Entraînement : 16 individus
* Test : 4 individus

Le modèle utilisé est un **Random Forest**, algorithme robuste et capable de capturer des interactions non linéaires même avec des variables peu nombreuses.

Cependant, le très faible nombre d’échantillons dans le test entraîne une forte instabilité des mesures de performance.

---

## **5. Résultats du Modèle : Analyse et Interprétation**

Les résultats observés sur le jeu de test sont les suivants :

### **5.1 Performance globale**

**Accuracy = 50 %**
Le modèle ne prédit correctement qu’un individu sur deux.
Une performance aussi faible ne permet pas de considérer le modèle comme fiable.

Cette faiblesse ne traduit pas un mauvais algorithme, mais surtout :

* le faible volume du test,
* la granularité réduite de la cible artificielle,
* l’insuffisance de données pour capturer des relations complexes.

---

### **5.2 Rapport de classification**

**Classe 0**

* Précision : 1.00
* Rappel : 0.33
* F1-score : 0.50
* Support : 3 individus

Le modèle identifie parfaitement les individus qu’il prédit en classe 0, mais il en oublie deux sur trois.
La sensibilité est donc très insuffisante.

**Classe 1**

* Précision : 0.33
* Rappel : 1.00
* F1-score : 0.50
* Support : 1 individu

Le modèle détecte tous les vrais individus classe 1, mais au prix d’un grand nombre de fausses alertes.
La précision faible indique un manque de sélectivité.

---

### **5.3 Matrice de confusion**

| Réel / Prédit | 0 | 1 |
| ------------- | - | - |
| Classe 0      | 1 | 2 |
| Classe 1      | 0 | 1 |

Interprétation :

* Deux individus réellement classe 0 sont classés à tort en classe 1.
* Aucun individu classe 1 n’est mal classé.
* Le modèle présente un biais vers la prédiction de la classe 1.

Ces erreurs proviennent principalement de l’échantillon très restreint.

---

## **6. Analyse Critique et Limites**

1. **Dataset extrêmement réduit**
   Le jeu de données ne contient que 20 individus, ce qui empêche un modèle d’apprendre des règles généralisables.

2. **Séparation Train/Test inadaptée**
   Un test composé de seulement 4 individus amplifie les distorsions statistiques.

3. **Cible artificielle**
   La création d’une variable binaire à partir d’une médiane réduit la richesse de l’information.

4. **Modèle trop complexe pour ce volume de données**
   Un Random Forest, bien que performant, n’a pas assez d’exemples pour stabiliser ses décisions.

---

## **7. Conclusion Générale**

Le projet démontre l’ensemble des étapes du cycle de vie d’un modèle de machine learning :
acquisition, nettoyage, exploration, modélisation et évaluation.

Cependant, la performance finale de 50 % montre que le modèle n’est pas fiable dans le contexte actuel.
Les limites proviennent essentiellement de la taille du dataset et de la nature artificielle de la cible.

Pour améliorer les résultats, il serait nécessaire d’utiliser :

* un jeu de données plus large,
* une cible mieux définie,
* une validation croisée,
* des modèles moins complexes ou des approches de régularisation.

---



