

 
 <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>

# KIHEL HAJAR

**Numéro d’étudiant** : 24010389
**Classe** : CAC2

---

# **Compte rendu d’Analyse : Prétraitement et Étude du Dataset Amazon Sales**

**Date :** 30 Novembre 2025
**Auteur :** KIHEL HAJAR


Voici une **page d’accueil simple et structurée** pour votre projet, construite à partir du contenu de votre compte-rendu  :

---

# **Prédiction des Notes Produits – Amazon Sales Dataset**

## **Description du Projet**

Ce projet a pour objectif de **prédire la note moyenne (`rating`) attribuée aux produits Amazon**, en se basant sur des caractéristiques telles que le prix, la réduction, le nombre de revues et la catégorie du produit.
Le travail inclut un **nettoyage approfondi des données**, une **analyse exploratoire**, la création de nouvelles caractéristiques, et l'entraînement de plusieurs modèles de régression afin d’évaluer leur capacité à estimer le `rating` réel du produit .

---

##  **Installation**

Pour exécuter le projet dans votre environnement local :

### **1. Cloner le projet**

```bash
git clone <url_du_projet>
cd <nom_du_dossier>
```

### **2. Créer un environnement**

```bash
python -m venv venv
source venv/bin/activate     # macOS / Linux
venv\Scripts\activate        # Windows
```

### **3. Installer les dépendances**

```bash
pip install -r requirements.txt
```

### **4. Lancer le notebook ou script**

```bash
jupyter notebook
```

ou

```bash
python main.py
```

---

##  **Résumé des Résultats**

Après tests de plusieurs modèles (Régression Linéaire, Random Forest, Gradient Boosting), le meilleur score a été obtenu avec le **GradientBoostingRegressor optimisé**, avec :

*  **R² = 0.1968**
*  **MAE = 0.1802**
*  **MSE = 0.0656** 

Ces résultats montrent que les variables numériques simples (prix, réduction, nombre de revues, catégorie) **expliquent moins de 20% de la variance réelle du rating**, indiquant que ces caractéristiques sont **faiblement prédictives**.

La conclusion principale :
Pour améliorer significativement la performance, il sera nécessaire d’exploiter les **données textuelles** du dataset (ex: *product_name, about_product, review_title*), notamment via des techniques de **NLP** telles que le *TF-IDF*, *Word Embeddings* ou l’analyse de sentiment .

---














