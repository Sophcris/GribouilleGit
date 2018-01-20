# 2048-lafabrique

[2048](http://gabrielecirulli.github.io/2048/) est un jeu [libre](https://fr.wikipedia.org/wiki/Logiciel_libre) (dont le code source est hébergé sur [github](https://github.com/gabrielecirulli/2048))
qui a tout de suite eu beaucoup de succès à sa sortie.

Il a été codé avec des technologies web et est donc compatible avec toutes les plateformes existantes (desktop et mobile).

Dans le cadre du cours de Javascript pour la fabrique du numérique, vous allez avoir à recoder entièrement ce jeu en partant de 0 (ou plutôt de 2 eheh).

Ce document décrit avec précision le fonctionnement du jeu, les différentes étapes du développement, les modalités de rendu ainsi que le barême qui sera appliqué pour la notation finale.

_Note : bien que le code source de ce projet soit libre et qu'il existe beaucoup d'autres clones disponible, n'essayez pas de le recopier. Je saurai voir en un clin d'oeil si ce code ne vient pas de vous !_

## Fonctionnement du jeu

2048 est un jeu assez simple mais suffisament compliqué pour que son développement vous prenne la tête quelques jours, voir plus :).

Voici le fonctionnement du jeu détaillé :
* Le jeu est contenu dans une grille de 4*4
* La partie commence avec 2 nombres positionnés aléatoirement dans la grille. Ces nombres sont généralement des 2 (dans 90% des cas), mais il peut s'agir de 4 aussi (dans 10% des cas)
* Il est possible de déplacer tous les nombres de la grille en utilisant les flèches du clavier (optionnellement Z, Q, S, D ou I, J, K, L) ou les mouvements de vos doigts sur un smartphone.
* Lors du déplacement de la grille :
    * Tous les nombres sont décalés dans la direction voulue
    * Lors de se décalement, si 2 nombres identiques se retrouvent côte à côte, ils sont alors "fusionné" en un seul nombre qui prend la place du nombre le plus loin dans la direction de la grille.
    * Un nombre "fusionné" prend comme valeur **la somme des deux des nombres.**
        * Attention, un chiffre "fusionné", ne peut pas se fusionner à nouveau dans le même déplacement !
        * Exemple : si sur une ligne il y a : "2 rien 2 4", lors d'un déplacement à droite, la ligne deviendra : "rien rien 4 4"
* Tant que la grille n'est pas remplit ou qu'elle permet encore des déplacement même remplit (ie il reste encore des chiffres à fusionner), il est possible de jouer
* Si le joueur atteint le chiffre fusionné de 2048, il a alors gagné mais peut encore continuer pour battre son meilleur score (je connais des personne qui sont allé à 8192, je ne sais pas comment elles ont fait)