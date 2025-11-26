
 
  
  <img src="photo-kihel hajar.jpeg" style="height:464px;margin-right:432px"/>
  

## kihel hajar

## N° apogée : 24010389

 ## Description générale de la base de données : Student Performance
 La base de données Student Performance a été élaborée par Paulo Cortez (Université du Minho, Portugal) et Alice Silva (École Secondaire Gabriel Pereira, Évora) dans le cadre d’une étude scientifique publiée en 2008. Elle provient du UCI Machine Learning Repository, une plateforme internationale de référence pour la recherche en intelligence artificielle. Cette base regroupe des informations académiques, sociales et comportementales d’élèves portugais du secondaire, inscrits dans deux écoles — Gabriel Pereira et Mousinho da Silveira — et suivant les cours de Mathématiques et de Portugais. L’objectif de cette étude est d’analyser les facteurs influençant la réussite scolaire et de modéliser la performance finale des élèves (note G3) à partir de variables personnelles (âge, sexe, absences, études des parents, temps d’étude, etc.). Le jeu de données comprend environ 33 variables et plus de 1 000 observations (395 en mathématiques et 649 en portugais). Il permet d’explorer les corrélations entre les comportements, le milieu familial et les résultats scolaires, tout en offrant un support utile pour la statistique descriptive, la prédiction de la réussite, et la mise en œuvre d’algorithmes de machine learning.


 <img src="graphe student-perfo.png" style="height:464px;margin-right:432px"/>


# 🧮 Analyse des distributions des variables numériques (Student Performance)

## 🎓 1. Distribution de l’âge
- La majorité des élèves ont **entre 15 et 18 ans**, avec un pic clair à **16–17 ans**.  
- Très peu d’élèves ont plus de 19 ans, ce qui suggère une population scolaire typique du **secondaire**.  
➡️ *Interprétation : la cohorte est homogène en âge, ce qui réduit l’influence de ce facteur sur les notes.*

---

## 📆 2. Distribution des absences
- La variable `Absences` est **fortement asymétrique à droite** :  
  beaucoup d’élèves ont **peu ou pas d’absences**, mais quelques-uns en ont **plus de 20 ou 30**, ce qui crée une longue queue.  
- Cela reflète une minorité d’élèves très souvent absents.  
➡️ *Interprétation : les absences sont rares pour la majorité, mais peuvent représenter un facteur critique pour un petit groupe (risque d’échec scolaire).*

---

## 🧮 3. Distribution des notes G1 (première période)
- La distribution est **centrée autour de 10–13/20**, légèrement asymétrique à gauche.  
- Peu d’élèves obtiennent des notes très faibles ou très élevées.  
➡️ *Interprétation : la majorité obtient des résultats moyens, traduisant une cohorte équilibrée sans extrêmes.*

---

## 📚 4. Distribution des notes G2 (deuxième période)
- La forme est similaire à G1, mais **légèrement plus concentrée** autour de 10–14/20.  
- Cela indique une **stabilisation ou légère amélioration** au fil de l’année.  
➡️ *Interprétation : les progrès entre G1 et G2 semblent modestes mais visibles.*

---

## 🏁 5. Distribution des notes G3 (note finale)
- La distribution est un peu plus **reserrée autour de 11–13**, avec moins de valeurs extrêmes.  
- Quelques élèves restent en échec (<5), mais la majorité est dans la moyenne.  
➡️ *Interprétation : la note finale G3 confirme une **progression cohérente** au fil des trimestres, avec une consolidation de la performance scolaire.*

---

## 📈 Synthèse visuelle générale

| Variable | Forme de distribution | Interprétation |
|-----------|----------------------|----------------|
| **Age** | Assez normale, centrée sur 16–17 ans | Population homogène |
| **Absences** | Très asymétrique (forte queue droite) | Quelques élèves très absents |
| **G1** | Légèrement asymétrique à gauche | Majorité de notes moyennes |
| **G2** | Distribution centrée sur 10–14 | Amélioration générale |
| **G3** | Légèrement resserrée, centrée sur 11–13 | Bonne stabilité finale |

---

## 🧠 Conclusion interprétative

> Les distributions montrent une population scolaire équilibrée en âge et en niveau académique.  
> La performance moyenne est stable au cours des périodes (G1 → G2 → G3).  
> Seule la variable **absences** se distingue par sa dispersion : une minorité d’élèves cumule beaucoup d’absences, ce qui pourrait expliquer certaines notes faibles observées.
