

---

# **requirements.txt (à copier dans GitHub)**

```
pandas
numpy
matplotlib
seaborn
jupyter
```

---

# Explication simple

Un fichier **requirements.txt** sert à :

* lister les librairies Python utilisées dans ton projet
* permettre à n'importe qui de les installer avec une seule commande :

```
pip install -r requirements.txt
```

C’est un standard obligatoire dans les projets GitHub pour assurer la reproductibilité.

---

# Pourquoi ces dépendances pour ton projet ?

| Librairie  | Rôle dans ton projet Amazon Sales               |
| ---------- | ----------------------------------------------- |
| pandas     | Manipulation et nettoyage du dataset            |
| numpy      | Calculs numériques nécessaires au prétraitement |
| matplotlib | Création de graphiques (si tu en ajoutes)       |
| seaborn    | Visualisations statistiques améliorées          |
| jupyter    | Exécuter le notebook .ipynb contenant l’analyse |

---

