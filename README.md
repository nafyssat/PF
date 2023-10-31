# PF
L’ADN est le code qui régule pratiquement toute activité biochimique des cellules des êtres vivants. Les séquences d’ADN sont formées à partir de quatre nucléotides : cytosine (C), guanine (G), adénine (A) et thymine (T). Ces nucléotides
sont également appelés bases nucléiques. Par exemple :
TATAAA contient 6 bases
TAATACGACTCACTATAG contient 18 bases
Le rôle de l’ADN est d’encoder les protéines produites par les cellules, une protéine
pouvant être vue comme l’une des briques de base du vivant. Chaque protéine est
encodée par un gène, une sous-partie d’une séquence d’ADN (une protéine donnée
pouvant par ailleurs être encodée par plusieurs gènes distincts).
Lorsqu’une certaine protéine est nécessaire à l’activité d’une cellule donnée, le
gène associé est lu et traduit en une séquence d’ARN messager 1
. Les ribosomes
décodent ensuite cette séquence pour effectuer la synthèse de la protéine cible.
Ce processus de traduction d’un gène en ARN suivi de la synthèse de la protéine
encodée par ce gène est appelé transcription 2
.
L’encodage d’information par l”ADN est un procédé si peu coûteux qu’il est
parfois envisagé comme un avenir possible pour le problème général du stockage
de données [2]. On estime que la biosphère contient 5.3(±3.6) × 1031 millions de
bases [3]. Le génome humain est stocké dans 23 paires de chromosomes, pour un
total de 3 × 109 paires of bases : déplié, il mesurerait presque 5 cm de long.
Du fait de sa taille, la manipulation d’une molécule d’ADN en laboratoire est
un problème loin d’être simple. La plus ancienne technique de séquençage d’un
brin d’ADN (i.e. déterminer sa séquence de nucléotides) est le séquençage shotgun,
découvert en 1979. L’idée est de découper un ensemble de copies d’un même brin
en fragments aléatoires (par exemple de longueurs 2, 10, 50, ou 150 milliers de
bases), puis de recomposer la séquence de ce brin par alignement de ces fragments.
Malgré sa simplicité, le séquençage shotgun est à la base du projet de séquençage
du génome humain lancé en 1990 et achevé en 2022. Un élément-clef de ce projet est
la mise en œuvre d’algorithmes d’alignements de chaînes [1], i.e. de programmes
cherchant à réaligner les fragments d’un brin obtenus par découpage aléatoire.
Sans surprise, compte tenu de l’essor des techniques de séquençage et de l’immense quantité d’ADN présente dans la biosphère, il existe aujourd’hui de nombreuses bases de données répertoriant des collections de gènes ainsi que leurs protéines associées. L’exemple le plus connu est sans doute celui-ci :
https://www.ncbi.nlm.nih.gov/
Outre des données brutes, ces bases proposent une masse considérable de métadonnées sur les séquences biologiques découvertes à ce jour. On pourra par exemple
consulter la page suivante, qui donne le détail de chaque protéine encodée par le
génome de la bactérie Escherichia coli :
https://www.ncbi.nlm.nih.gov/nuccore/NZ_MT263755.1
L’extraction rapide des informations d’une telle page relève d’une nécessité pratique : les expressions régulières se prètent très efficacement à ce rôle. Vous les avez
déjà rencontrées dans l’usage d’outils tels que sed, awk, and grep.
Objectif du projet. Ce projet est inspiré par les problématiques soulevées cidessus. La première partie porte sur les problèmes de l’extraction de gènes et de la
reconstruction d’une séquence d’ADN (ou plus modestement, celui du calcul de ce
qu’on appelle la séquence consensus d’un ensemble de fragments – nous ignorerons
ici le problème de leur alignement). La seconde partie porte sur les expressions
régulières.
Remarques. Le niveau de difficulté des exercices est indiqué par zéro (facile)
une (? difficulté moyenne) ou deux étoiles (?? plus difficile). N’hésitez pas à poster
des questions (et non des réponses !) sur le sujet en écrivant à la liste de diffusion
de PF5 :
l3.pf5.info@listes.u-paris.fr
3 Analyse de brins d’ADN
Comme indiqué dans l’introduction, un brin d’ADN forme une séquence de
bases nucléiques. Les quatre bases nucléiques, représentées par les lettres A (adénine), T (thymine), G (guanine), et C (cytosine), seront représentées par le type
OCaml suivant :
✞ ☎
1 type base = A | C | G | T | WC
✝ ✆
Notons que ce type possède une cinquième valeur possible, WC (pour « Wild Card »),
représentant une base inconnue (e. g. qui n’a pu être correctement identifiée lors
du séquençage). Un brin d’ADN sera représenté par une liste de bases :
✞ ☎
1 type dna = base list
✝ ✆
Dans cette section, il vous est demandé d’implémenter quelques fonctions génériques de manipulation de listes qui pourront être utiles pour la suite. Chaque
fonction peut bien sûr se servir des précédentes.
3.1 Échauffement
##Exercice 3.0. Écrire une fonction
✞ ☎
1 explode : string -> char list
✝ ✆
qui convertit une chaîne de caractères en une liste de caractères. Par exemple :
explode "Hello!" = ['H', 'e', 'l', 'l', 'o', '!']
Exercice 3.1. Écrire une fonction
✞ ☎
1 base_of_char : char -> base
✝ ✆
qui convertit un caractère en base nucléique. Les caractères 'A', 'T', 'G',
'C' seront respectivement convertis en A, T, G, C. Tout autre caractère sera
converti en WC. Par exemple :
base_of_char 'G' = G et base_of_char '.' = WC.
