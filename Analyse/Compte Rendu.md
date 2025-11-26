
 
 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d'étudiant** : 24010389  
**Classe** : CAC2

<br clear="left"/>

---
# Compte rendu
## Analyse prédictive du jeux de donnée "COVID-19 Pandemic"

**Date :** 26 Novembre 2025

---


# À propos du jeu de données COVID-19


Le jeu de données COVID-19 rassemble des informations essentielles liées à l’évolution de la pandémie : nombre de cas confirmés, guérisons, décès, taux de vaccination, résultats de tests ou encore caractéristiques démographiques des populations touchées. Ces données sont généralement collectées par des institutions de santé publiques telles que l’OMS, les ministères de la santé ou des laboratoires nationaux, afin d’assurer un suivi quotidien et précis de la situation sanitaire mondiale.

Ce dataset est largement utilisé en data science car il permet d’analyser la propagation du virus, d’identifier les périodes critiques et de mesurer l’impact des politiques sanitaires comme le confinement, la distanciation sociale ou la vaccination. Les scientifiques et analystes peuvent visualiser des courbes épidémiologiques, suivre les tendances temporelles ou comparer les dynamiques de transmission entre différents pays et régions.

Grâce à sa richesse, le jeu de données COVID-19 permet aussi de construire des modèles prédictifs capables d’anticiper l’évolution des cas, d’évaluer les risques futurs ou d’optimiser les ressources médicales. Il constitue ainsi un outil essentiel pour comprendre les mécanismes de diffusion du virus, appuyer la prise de décision et contribuer à la gestion de crises sanitaires similaires dans l’avenir.



### Prétraitement • Régression Linéaire Simple • Régression Multiple • Régression Polynomiale

---

## 1. Objectif Général du Projet

L’objectif de ce projet est d’analyser une base de données mondiale concernant la pandémie du Covid-19.  
Cette base contient des informations sur le nombre de cas confirmés, les décès, les personnes guéries, les cas actifs, la région OMS, ainsi que des données géographiques comme la latitude et la longitude.

Nous avons appliqué plusieurs méthodes statistiques et de machine learning pour comprendre :

- Quelles variables influencent le plus les cas confirmés ?
- Quelle est la relation entre les décès et les cas confirmés ?
- Comment plusieurs facteurs combinés expliquent la propagation du Covid-19 ?
- Les relations sont-elles linéaires ou non linéaires ?

Ce compte-rendu résume toutes les étapes du projet, du traitement des données jusqu’aux modèles de régression, avec des explications simples et progressives.

---

## 2. Étape 1 : Prétraitement des Données  
###  Pourquoi cette étape est importante ?

Avant de construire un modèle, il est essentiel de préparer les données.  
Des données mal nettoyées peuvent donner des modèles incorrects, biaisés ou inutilisables.

### Actions réalisées

1. **Conversion des dates**  
   La colonne `Date` a été convertie au format datetime afin de faciliter les analyses temporelles.

2. **Vérification des valeurs manquantes**  
   Nous avons inspecté toutes les colonnes pour identifier les valeurs absentes ou incohérentes.  
   Ces valeurs peuvent fausser les modèles, donc cette étape est indispensable.

3. **Sélection des colonnes pertinentes**  
   Seules les colonnes utiles pour l’analyse ont été conservées :  
   - Confirmed  
   - Deaths  
   - Recovered  
   - Active  
   - Lat / Long  
   - WHO Region  
   - Country/Region

4. **Analyse de la structure du DataFrame**  
   Le dataset final contient **49 068 lignes et 9 colonnes**, ce qui représente une quantité suffisante pour avoir des résultats fiables.

### Interprétation du prétraitement

Grâce à cette étape, les données sont propres, cohérentes et prêtes à être utilisées dans différents modèles statistiques.  
Sans ce prétraitement, les résultats auraient été erronés ou peu significatifs.

---

## 3. Étape 2 : Régression Linéaire Simple  
### Objectif de cette analyse

Comprendre si les décès (`Deaths`) peuvent expliquer à eux seuls l’évolution des cas confirmés (`Confirmed`).  
C’est une première approche simple qui observe la relation entre deux variables seulement.

###  Ce que nous avons fait

- Diviser les données entre un **ensemble d’entraînement** et un **ensemble de test**.
- Construire un modèle linéaire qui apprend la relation entre les décès et les cas confirmés.
- Visualiser le nuage de points et la droite de régression.

### Résultats obtenus

Le modèle montre une relation **positive** :  
> Lorsque le nombre de décès augmente, le nombre de cas confirmés augmente également.

Cela peut paraître logique : plus il y a de cas, plus il y a de risques de décès.

### Interprétation

- Le modèle explique une partie de la pandémie, mais uniquement à travers les décès.
- Or, la pandémie dépend de nombreux autres facteurs :  
  tests réalisés, politiques sanitaires, variant, comportements sociaux…
- Donc cette régression simple est utile seulement pour avoir une première idée.

---

## 4. Étape 3 : Régression Linéaire Multiple  
### Pourquoi utiliser plusieurs variables ?

La pandémie Covid-19 est un phénomène complexe.  
Il n’est pas possible d’expliquer les cas confirmés avec une seule variable.

C’est pourquoi nous ajoutons d’autres variables explicatives :

- **Deaths** (décès)  
- **Recovered** (guérisons)  
- **Active** (cas actifs)  
- **Lat / Long** (position géographique)

### Ce que fait ce modèle

Il étudie l’effet combiné de plusieurs facteurs sur le nombre de cas confirmés.  
Cela permet de voir quelles variables ont le plus d’impact.

### Résultats importants

- Les décès et les cas actifs ont une forte influence positive sur les cas confirmés.  
  → plus une région est touchée, plus ces chiffres évoluent ensemble.

- Les guérisons ont un effet variable selon le contexte.

- La localisation (latitude / longitude) influence aussi la propagation  
  (densité, climat, frontières, population…).

### Interprétation

La régression multiple donne une image plus complète de la pandémie.  
Elle montre que plusieurs variables sont nécessaires pour décrire correctement le phénomène.

C’est le modèle **le plus équilibré** pour ce dataset.

---

## 5. Étape 4 : Régression Polynomiale  
### Pourquoi passer à un modèle non linéaire ?

La pandémie n’évolue pas de manière linéaire.  
Les relations entre cas confirmés et décès suivent souvent des formes courbées :

- croissance rapide  
- pic épidémique  
- décroissance  
- vagues successives  

La régression polynomiale de degré 2 permet de capturer ces courbes.

### Ce que fait ce modèle

- On transforme la variable `Deaths` en plusieurs puissances (1, 2).  
- On construit un modèle non linéaire.  
- On obtient une courbe qui suit mieux la répartition des données.

### 📊 Résultats

- Le modèle s’adapte mieux que la régression simple.  
- Il prédit plus précisément les cas confirmés, surtout dans les zones très touchées.

### Interprétation

La régression polynomiale montre que le lien entre décès et cas confirmés est **non linéaire**.  
Ce type de modèle est plus réaliste lors d’une pandémie où la croissance est souvent exponentielle.

---

## 6. Comparaison des Modèles

Voici un résumé clair :

| Modèle | Points forts | Limites |
|-------|--------------|---------|
| **Régression simple** | Très facile à comprendre | Trop simpliste |
| **Régression multiple** | Plus réaliste, utilise plusieurs facteurs | Peut souffrir de multicolinéarité |
| **Régression polynomiale** | Capture la non-linéarité | Risque d'overfitting si trop complexe |

###  Meilleur modèle observé  
La **régression multiple** : elle offre le meilleur compromis entre simplicité, précision et interprétabilité.

---

## 7. Conclusion Générale du Projet

Cette analyse montre que :

- La pandémie Covid-19 dépend de plusieurs facteurs combinés.
- Un modèle simple ne suffit pas pour capturer la dynamique réelle.
- La régression multiple est la plus efficace avec un dataset global et varié.
- La régression polynomiale est utile pour modéliser les phases rapides de propagation.
- Pour aller encore plus loin, on pourrait utiliser :  
  - Random Forest  
  - XGBoost  
  - Réseaux neuronaux  
  - Modèles séquentiels (ARIMA, LSTM)

Ce projet permet de mieux comprendre les relations statistiques autour du Covid-19 et de poser les bases pour des analyses plus avancées.

---



