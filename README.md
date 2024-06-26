# Mini-projet – Ensemble Learning
## Contexte
Ce mini-projet a été réalisé lors de ma dernière année en tant qu'étudiant ingénieur spécialisé en Intelligence Artificielle et Data Science à l'[ESIEA](https://www.esiea.fr/), une école d'ingénieurs basée à Paris.

## Objectif
L'objectif de ce projet est d'étudier, d'évaluer et de comparer les performances de différentes techniques d'ensemble (AdaBoost, bagging, et forêts aléatoires) en termes de taux de reconnaissance (accuracy), de temps d'apprentissage et de temps d'inférence pour prédire la qualité d'une bière en utilisant des données quantitatives.   
Ces données incluent des mesures scientifiques telles que l'acidité, le sucre résiduel, les chlorures, le dioxyde de soufre, la densité, le pH, les sulfates et le pourcentage d'alcool.

Ci-dessous une description des colonnes du jeu de données.
| Colonne                | Description                                                      |
|------------------------|------------------------------------------------------------------|
| `fixed acidity`        | Acidité fixe présente dans la bière                              |
| `volatile acidity`     | Acidité volatile présente dans la bière                          |
| `citric acid`          | Quantité d'acide citrique dans la bière                          |
| `residual sugar`       | Quantité de sucre résiduel dans la bière                         |
| `chlorides`            | Concentration de chlorures dans la bière                         |
| `free sulfur dioxide`  | Quantité de dioxyde de soufre libre dans la bière                |
| `total sulfur dioxide` | Quantité totale de dioxyde de soufre dans la bière               |
| `density`              | Densité de la bière                                              |
| `pH`                   | Niveau d'acidité ou d'alcalinité de la bière                     |
| `sulphates`            | Concentration de sulfates dans la bière                          |
| `alcohol`              | Taux d'alcool dans la bière                                      |
| `quality`              | Note de qualité de la bière, sur une échelle de 1 à 10           |

## Structure du projet
```plaintext
/mini-projet-ensemble-learning
│
├── beer_quality.csv                       # Jeu de données du projet
├── study_ensemble_learning.ipynb          # Notebook de l'étude
└── Mini-projet Ensemble Learning.pdf      # Rapport du projet
```

# Sujet
## Attention
- Les parties ne sont pas indépendantes. Si vous tirez des conclusions dans la partie $p$, ne les oubliez pas quand vous commencez la partie $p+1$.
- Pensez à mesurer les temps d’apprentissage et d’inférence de chaque solution.

## A. Base des données
La base de données « beer quality » comporte 1600 exemples décrits par 11 caractéristiques quantitatives. L’objectif est d’évaluer, sachant ces variables, la qualité d’une bière, évaluée de 1 (sans commentaire !) à 10 (particulièrement excellente). 

1. Charger la base et la séparer en deux : la matrice $X$ des observations et le vecteur $y$ des labels.
2. Diviser la base de données en deux sous-ensembles d’apprentissage et de test (70/30). Analyser rapidement les variables prédictives `X_train` et la variable à prédire `y_train` (quality).

## B. Classification binaire
1. Créer une nouvelle variable quantitative `ybin` à deux modalités : 
    - 0 : mauvaise qualité : $y < m$
    - 1 : bonne qualité : $y >= m$
    - en fonction de la médiane $m$ de la variable $y$. Dans cette partie, c’est `ybin` qu’on cherchera à prédire.

2. Optimiser rapidement un arbre de décision pour réaliser la classification en faisant une recherche aléatoire (random search).

3. Entraîner un ensemble d’arbres de décision « faibles » (peu, voire très peu profonds) à l’aide de l’algorithme AdaBoost. Analyser les performances en fonction des différents paramètres :
    - En particulier, tracer les courbes accuracy en fonction de `n_estimators` pour `max_depth = 1`, en apprentissage et en validation.
    - Tracer la courbe accuracy en fonction de `n_estimators` pour `max_depth = 5`, en apprentissage et en validation.
    - Choisir la solution optimale.
    - Peut-on mesurer l’importance d’une caractéristique dans la décision AdaBoost ? Expliquez. Afficher les variables par ordre d’importance.
    - Conclure sur le biais et la variance de l’algorithme.

## C. Classification multiclasse
1. Créer une nouvelle variable quantitative `ymulti` discrète à 3 modalités : qualité basse (0), moyenne (1) ou élevée (2).

2. Déterminer les effectifs des différentes classes. Si nécessaire, équilibrer les données d’apprentissage par sous-échantillonnage ou augmentation de données (SMOTE). Dans la suite, on présentera les résultats obtenus avec et sans équilibrage.

### Partie 1
3. Entraîner un réseau de neurones à une couche cachée pour effectuer cette tâche de classification, avec early stopping sur la base de validation. L’optimiser rapidement en prenant soin d’éviter l’overfitting. Étudier les matrices de confusion des réseaux optimaux dans le cas des données déséquilibrées puis, équilibrées. Conclure.

4. Faire un bagging en utilisant comme classifieur de base le réseau de neurones.
    - Tracer la courbe accuracy en fonction de `n_estimators`, en apprentissage et en validation.
    - Choisir le modèle optimal.
    - Conclure sur le biais et la variance.

### Partie 2
5. Entraîner une forêt aléatoire :
    - Tracer la courbe accuracy en fonction de `n_estimators` pour `max_depth = None`, en apprentissage et en test.
    - Faire une recherche aléatoire (random search) pour optimiser les paramètres `max_depth` et `n_estimators`. Choisir les paramètres optimaux et donner les performances en apprentissage et en test. Comparer avec les résultats obtenus précédemment (matrice de confusion sur les données déséquilibrées et équilibrées).
    - Choisir le modèle optimal.
    - Afficher les variables par ordre d’importance. Retrouve-t-on les mêmes variables qu’en B.3 ?
    - Conclure sur le biais et la variance.

## D. Conclusion générale sur les méthodes d’ensemble
Comparer les différentes techniques mises en œuvre en termes de performances (accuracy, temps d’apprentissage et d’inférence) en rassemblant les résultats dans un graphe ou un tableau. Conclure.
