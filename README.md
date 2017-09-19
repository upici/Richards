# Pour l'évaluation

-   **Prendre 10 min à chaque fin de séance pour écrire ce qu'on a fait dans le
    fichier [./Rapports.md](./Rapports.md)**
-   le rapport terminal doit être rédiger en Latex dans le répertoire [./rapports](rapports)

# Résolution de l'équation de Richards

## Objectif final, très ambitieux.

L'équation de Richards, sous sa forme habituelle en hydrogéologie, est une
équation parabolique non linéaire, \( \partial_t \theta(\psi) - \mathop{div}(
K(\psi)\nabl(\psi+z) ) = 0\). Elle modélise l'écoulement de l'eau dans un
sous-sol poreux, par l'intermédiaire de la variable \(\psi(t,x)\) appelée teneur
en eau et exprimé en m, voir les 2 premiers chapitres de la thèse de V. Baron
pour une introduction. La fonction \(\theta\) représente la teneur en eau, alors
que la fonction \(K(\psi)\) modélise les caractéristiques mécaniques du milieu
poreux dans lequel l'eau s'écoule. Ces deux fonctions sont données et l'inconnue
recherchée est le fonction \(\psi\).

L'objectif final est de simuler l'infiltration d'eau dans un domaine
unidimensionnel (suivant \(z\)) représentant un sous-sol poreux d'une dizaine de
mètres de profondeur, initialement sec et soumis à une pression d'eau
constante. 

Pour ce type d'équation, les schémas volume finis sont assez simple à mettre en
oeuvre, mais une discrétisation implicite en temps est nécessaire. La résolution
fait donc intervenir une méthode de Newton et la résolution de systèmes
linéaires. 

Les paramètres de la discrétisation et de la résolution sont nombreux. On
s'intéressera en particulier au cas-test de Polman (voir [Celia, Bouloutas,
Water Resources Research, 1990]).

## Première partie : recherche de resources, documentation

1.  L'équation modèle associée à ce problème est l'équation parabolique linéaire
    \(\partial_t u - \partial_x(a(x)\partial u) = f(t,x)\), avec un coefficient non
    constant \(a(x)\), qui pourrait même être discontinu. Trouver et synthétiser de
    la documentation sur ce type d'équation dont il s'agit. Quelles conditions
    aux limite peut on utiliser ? Quelles sont les conditions sur \(a(x)\) pour
    pouvoir la résoudre, etc ?
2.  Trouver de la documentation sur les méthodes de volumes finis pour cette
    équation. Qu'est-ce qui se passe lorsque \(a(x)\) est discontinu ?
3.  Quels types de schémas en temps peut-on envisager en combinaison avec un
    schéma volumes finis pour cette équation ? Détailler le système d'équation
    que l'on doit résoudre à chaque pas de temps, et les méthodes possibles pour
    le résoudre. Attention, dans l'implémentation des schémas volumes finis, il
    est habituel de ne pas calculer explicitement les matrices qui apparaissent.

## Deuxième partie : programmation dans un cas simplifié

L'objectif est de biencomprendre l'implémentation des méthodes, avant de
s'attaquer au problème complet.

1.  Détailler l'architecture du code à implémenter, en essayant d'avoir un code
    modulaire et extensible facilement. Entrées et sorties ? Structuration du
    code en fichiers ? Quels outils de l'ensemble scipy/numpy ?
2.  Dans le cas \(a(x)=1\), on retrouve l'équation de la chaleur. Déterminer des
    situations pour lesquelles on peut calculer des solutions analytiques. Nous
    les utiliserons pour valider notre implémentation.
3.  Programmer la résolution du problème dans le cas linéaire, et vérifier cette
    implémentation à l'aide des tests de la question 2.

## Troisième partie : le cas général

On va généraliser le code produit dans la partie précédente au cas non-linéaire.

1.  Que se passe-t-il lors de la discrétisation de l'équation par volumes finis ?
    Quelles conséquence cela a-t-il sur le système à résoudre à chaque pas de
    temps ? Sur l'algorithme utilisé pour le résoudre ?
2.  Déterminer comment le code produit précédant peut se généraliser au cas
    non-linéaire. Qu'est-ce qui change ? Quels sont les fichiers à modifier ?
    Comment pourrait-on trouver des solutions analytiques permettant de valider
    l'implémentation ?
3.  Produire le code de résolution du problème et le tester,

## refs

À compléter dans le répertoire [./refs](./refs)
