
# Analyse de Séquences d'ADN

Ce projet porte sur l'analyse de séquences d'ADN et l'utilisation d'expressions régulières pour extraire des informations pertinentes. Il s'articule en deux parties principales.

## Introduction

L'ADN (acide désoxyribonucléique) est le code qui régule pratiquement toute activité biochimique des cellules des êtres vivants. Les séquences d'ADN sont formées à partir de quatre nucléotides : cytosine (C), guanine (G), adénine (A) et thymine (T). Ces nucléotides sont également appelés bases nucléiques. Par exemple : "TATAAA" contient 6 bases, tandis que "TAATACGACTCACTATAG" contient 18 bases.

Le rôle de l'ADN est d'encoder les protéines produites par les cellules, une protéine pouvant être vue comme l'une des briques de base du vivant. Chaque protéine est encodée par un gène, une sous-partie d'une séquence d'ADN (une protéine donnée pouvant par ailleurs être encodée par plusieurs gènes distincts). Lorsqu'une certaine protéine est nécessaire à l'activité d'une cellule donnée, le gène associé est lu et traduit en une séquence d'ARN messager. Les ribosomes décodent ensuite cette séquence pour effectuer la synthèse de la protéine cible. Ce processus de traduction d'un gène en ARN suivi de la synthèse de la protéine encodée par ce gène est appelé transcription.

## Stockage de Données

L'encodage d'information par l'ADN est un procédé si peu coûteux qu'il est parfois envisagé comme un avenir possible pour le problème général du stockage de données. On estime que la biosphère contient 5.3(±3.6) × 10^31 millions de bases. Le génome humain est stocké dans 23 paires de chromosomes, pour un total de 3 × 10^9 paires de bases : déplié, il mesurerait presque 5 cm de long. Du fait de sa taille, la manipulation d'une molécule d'ADN en laboratoire est un problème loin d'être simple.

## Séquençage d'ADN

La plus ancienne technique de séquençage d'un brin d'ADN (c'est-à-dire déterminer sa séquence de nucléotides) est le séquençage shotgun, découvert en 1979. L'idée est de découper un ensemble de copies d'un même brin en fragments aléatoires (par exemple de longueurs 2, 10, 50, ou 150 milliers de bases), puis de recomposer la séquence de ce brin par alignement de ces fragments. Malgré sa simplicité, le séquençage shotgun est à la base du projet de séquençage du génome humain lancé en 1990 et achevé en 2022. Un élément-clé de ce projet est la mise en œuvre d'algorithmes d'alignements de chaînes, c'est-à-dire de programmes cherchant à réaligner les fragments d'un brin obtenus par découpage aléatoire.

## Bases de Données

Sans surprise, compte tenu de l'essor des techniques de séquençage et de l'immense quantité d'ADN présente dans la biosphère, il existe aujourd'hui de nombreuses bases de données répertoriant des collections de gènes ainsi que leurs protéines associées. L'exemple le plus connu est sans doute celui-ci : [Base de Données NCBI](https://www.ncbi.nlm.nih.gov/)

Outre des données brutes, ces bases proposent une masse considérable de métadonnées sur les séquences biologiques découvertes à ce jour. On pourra par exemple consulter la page suivante, qui donne le détail de chaque protéine encodée par le génome de la bactérie Escherichia coli : [Protéines d'Escherichia coli](https://www.ncbi.nlm.nih.gov/nuccore/NZ_MT263755.1)

L'extraction rapide des informations d'une telle page relève d'une nécessité pratique : les expressions régulières se prêtent très efficacement à ce rôle. Vous les avez déjà rencontrées dans l'usage d'outils tels que `sed`, `awk`, et `grep`.

## Objectif du Projet

Ce projet est inspiré par les problématiques soulevées ci-dessus. La première partie porte sur les problèmes de l'extraction de gènes et de la reconstruction d'une séquence d'ADN (ou plus modestement, celui du calcul de ce qu'on appelle la séquence consensus d'un ensemble de fragments – nous ignorerons ici le problème de leur alignement). La seconde partie porte sur les expressions régulières.

## Remarques

Le niveau de difficulté des exercices est indiqué par zéro (facile) une (difficulté moyenne) ou deux étoiles (plus difficile). N'hésitez pas à poster des questions (et non des réponses !) sur le sujet en écrivant à la liste de diffusion de PF5 : [l3.pf5.info@listes.u-paris.fr](mailto:l3.pf5.info@listes.u-paris.fr)

## Analyse de Brins d'ADN

Comme indiqué dans l'introduction, un brin d'ADN forme une séquence de bases nucléiques. Les quatre bases nucléiques, représentées par les lettres A (adénine), T (thymine), G (guanine), et C (cytosine), seront représentées par le type OCaml suivant :

```ocaml
type base = A | C | G | T | WC
