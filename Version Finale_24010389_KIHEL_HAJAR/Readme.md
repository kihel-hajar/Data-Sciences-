

---

<img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Modélisation de l’Impact de la Qualité de l’Air sur la Santé**

**Date :** 03 Décembre 2025
**Auteur :** KIHEL HAJAR

---

Voici une **page d’accueil claire et structurée** pour le projet **Air Quality – Health Impact**, rédigée dans un style académique et professionnel.

---

# **Prédiction de l’Impact Sanitaire – Air Quality Dataset**

## **Description du Projet**

Ce projet a pour objectif de **prédire l’impact sanitaire de la pollution de l’air**, à partir de différentes **variables environnementales** liées à la qualité de l’air.
L’objectif principal est d’analyser si les niveaux de pollution mesurés peuvent être utilisés pour **estimer automatiquement un indice d’impact sur la santé**.

Le travail comprend :

* le **nettoyage et la préparation des données**,
* la **gestion des valeurs manquantes**,
* une **analyse exploratoire des données (EDA)**,
* l’entraînement d’un **modèle de régression** afin d’évaluer sa capacité à prédire l’impact sanitaire réel.

---

## **Installation**

Pour exécuter le projet dans un environnement local :

### **1. Cloner le projet**

```bash
git clone <url_du_projet>
cd <nom_du_dossier>
```

### **2. Créer un environnement virtuel**

```bash
python -m venv venv
source venv/bin/activate     # macOS / Linux
venv\Scripts\activate        # Windows
```

### **3. Installer les dépendances**

```bash
pip install -r requirements.txt
```

### **4. Lancer le notebook ou le script**

```bash
jupyter notebook
```

ou

```bash
python main.py
```

---

## **Résumé des Résultats**

Après entraînement du modèle **RandomForestRegressor**, les performances obtenues sont les suivantes :

* **R² = 0.6827**
* **RMSE = 0.4124**
* **MSE = 0.1701**

Ces résultats montrent que le modèle est capable d’expliquer environ **68 % de la variabilité de l’impact sanitaire**, ce qui indique une **relation significative entre la qualité de l’air et la santé**.

La conclusion principale est la suivante :
Les données environnementales permettent de prédire l’impact sanitaire de manière globalement fiable, même si le phénomène reste complexe et influencé par d’autres facteurs externes.

Des améliorations futures pourraient inclure :

* l’ajout de **validation croisée**,
* l’étude de l’**importance des variables**,
* la comparaison avec d’autres modèles de régression,
* l’intégration de données temporelles ou démographiques.

---


