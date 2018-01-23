# 2048-lafabrique

1. [Introduction](#introduction)
2. [Fonctionnement du jeu](#fonctionnement-du-jeu)
3. [Etapes de développement](#etapes-de-developpement)
    1. [Arriver à gérer l'affichage de la grille en Javascript](#arriver-a-gerer-l'affichage-de-la-grille-en-Javascript)
    2. [Placement aléatoire des nombres](#placement-aleatoire-des-nombres)
    3. [Affichage](#affichage)
    4. [Bouton "Nouvelle partie"](#bouton-nouvelle-partie)
    5. [Détecter les déplacements](#detecter-les-deplacements)
    6. [Déplacer les nombres dans une direction](#deplacer-les-nombres-dans-une-direction)
    7. [Fusionner les nombres](#fusionner-les-nombres)
    8. [Gérer toutes les directions](#gerer-toutes-les-directions)
    9. [Gérer le game over](#gerer-le-game-over)
    10. [Gérer les scores](#gerer-les-scores)
4. [Les commandements de maître Yoda](#les-commandements-de-maître-Yoda)
    1. [Git tu utiliseras](#git-tu-utiliseras)
        1. [Les commandes de base](#les-commandes-de-base)
    2. [Sur Gitlab ton projet tu rendras](#sur-Gitlab-ton-projet-tu-rendras)
    3. [Formater ton code tu dois](#formater-ton-code-tu-dois)
    4. [Eslint ton code valide sera](#eslint-ton-code-valide-sera)
    5. [Bryan is in the kitchen](#bryan-is-in-the-kitchen)
    6. [Small is beautifull](#small-is-beautifull)
    7. [Jamais tu ne copieras](#jamais-tu-ne-copieras)
    8. [Du javascript récent tu utiliseras](#du-javascript-recent-tu-utiliseras)
5. [Barème](#bareme)
    1. [Forme](#forme)
        1. [Rendu à temps](#rendu-à-temps)
        2. [Rendu dans les bonnes modalités](#rendu-dans-les-bonnes-modalites)
        3. [Plusieurs commits avec messages explicites](#plusieurs-commits-avec-messages-explicites)
        4. [Code écrit dans un anglais compréhensible](#code-ecrit-dans-un-anglais-comprehensible)
        5. [Fonctions pas trop grosses](#fonctions-pas-trop-grosses)
        6. [Pas de duplication de code](#pas-de-duplication-de-code)
        7. [Eslint OK](#eslint-ok)
        8. [Code formaté](#code-formate)
        9. [Module ES6](#module-es6)
    2. [Fond](#fond)
        1. [Position aléatoire des 2 premiers nombres](#position-aleatoire-des-2-premiers-nombres)
        2. [Déplacement des tuiles avec les touches au moins dans une direction](#deplacement-des-tuiles-avec-les-touches-au-moins-dans une direction)
        3. [Fusion des nombres fonctionnelle au moins dans une direction](#fusion-des-nombres-fonctionnelle-au-moins-dans-une-direction)
        4. [Apparition d'une nouvelle tuile après un déplacement](#apparition-d'une-nouvelle-tuile-apres-un-deplacement)
        5. [Gestion du game over](#gestion-du-game-over)
        6. [Message quand on a gagné](#message-quand-on-a-gagne)
        7. [Déplacement fonctionnel dans toutes les directions](#deplacement-fonctionnel-dans-toutes-les-directions)
        8. [Fusion des nombres fonctionnelle dans toutes les directions](#fusion-des-nombres-fonctionnelle-dans-toutes-les-directions)
        9. [Jeu "joli" et original](#jeu-joli-et-original)
        10. [Utilisation des bonnes classes CSS](#utilisation-des-bonnes-classes-CSS)
    3. [Bonus](#bonus)
        1. [Sauvegarde des meilleurs scores](#sauvegarde-des-meilleurs-scores)
        2. [Sauvegarde de la partie en cours](#sauvegarde-de-la-partie-en-cours)
        3. [Animation sur les déplacements](#animation-sur-les-deplacements)
        4. [Animation pour les nouvelles tuiles](#animation-pour-les-nouvelles-tuiles)
        5. [Gestion des événements touch](#gestion-des-événements-touch)


## Introduction

[2048](http://gabrielecirulli.github.io/2048/) est un jeu [libre](https://fr.wikipedia.org/wiki/Logiciel_libre) (dont le code source est hébergé sur [github](https://github.com/gabrielecirulli/2048))
qui a tout de suite eu beaucoup de succès à sa sortie.

Il a été codé avec des technologies web et est donc compatible avec toutes les plateformes existantes (desktop et mobile).

Dans le cadre du cours de Javascript pour la fabrique du numérique, vous allez avoir à recoder entièrement ce jeu en partant de 0 (ou plutôt de 2 eheh).

Ce document décrit avec précision le fonctionnement du jeu, les différentes étapes du développement, les modalités de rendu (ou "commandements de Yoda") ainsi que le barême qui sera appliqué pour la notation finale.

_Note : bien que le code source de ce projet soit libre et qu'il existe beaucoup d'autres clones disponible, n'essayez pas de le recopier. Je saurai voir en un clin d'oeil si ce code ne vient pas de vous !_


## Fonctionnement du jeu

2048 est un jeu assez simple mais suffisament compliqué pour que son développement vous prenne la tête quelques jours, voir plus :).

Voici le fonctionnement du jeu détaillé :

* Le jeu est contenu dans une grille de 4*4
* La partie commence avec 2 nombres positionnés aléatoirement dans la grille. Ces nombres sont généralement des 2 (dans 90% des cas), mais il peut s'agir de 4 aussi (dans 10% des cas)
* Il est possible de déplacer tous les nombres de la grille en utilisant les flèches du clavier (optionnellement Z, Q, S, D ou I, J, K, L) ou les mouvements de vos doigts sur un smartphone.
* Lors du déplacement de la grille :
    * Tous les nombres sont décalés dans la direction voulue
    * Lors de ce décalement, si 2 nombres identiques se retrouvent côte à côte, ils sont alors "fusionné" en un seul nombre qui prend la place du nombre le plus loin dans la direction de la grille.
    * Un nouveau nombre est généré aléatoire même si aucun nombre ne bouge après un décalement (ie ils étaient déjà tous décaler dans la direction)
    * Un nombre "fusionné" prend comme valeur **la somme des deux des nombres.**
    * Cette valeur s'ajoute alors au score de la partie. Ex: on fusionne deux nombres 4, ce qui donne un chiffre fusionné 8 et ajoute ainsi 8 au score.
    * Attention, un chiffre "fusionné", ne peut pas se fusionner à nouveau dans le même déplacement !
    * Exemple : si sur une ligne il y a : "2 rien 2 4", lors d'un déplacement à droite, la ligne deviendra : "rien rien 4 4"
    * Après chaque déplacement, un nouveau chiffre apparait aléatoirement aux endroits vides de la grille selon les mêmes modalités que le chiffre de départ (90% de chance de 2 et 10% de 4).
    * S'il n'y a eu aucun déplacement ou aucune fusion, alors le nouveau chiffre n'apparait pas.
    * S'il n'y a plus de place pour que le nouveau chiffre apparaisse, alors la partie est perdue.
* Tant que la grille n'est pas remplit ou qu'elle permet encore des déplacement même remplit (ie il reste encore des chiffres à fusionner), il est possible de jouer.
* Si la grille et totalement remplit et qu'aucun déplacement n'est possible dans aucune direction, alors la partie est perdue.
* Si le joueur atteint le chiffre fusionné de 2048, **il a alors gagné** mais peut encore continuer pour battre son meilleur score (je connais des personne qui sont allé à 8192, je ne sais pas comment elles ont fait)

## Etapes de développement

Pour vous aider dans la mise en place du projet, j'ai découpé le développement en plusieurs étapes. Vous n'êtes pas obligé de les suivre elles sont à titre indicatif :

### Arriver à gérer l'affichage de la grille en Javascript

Au tout départ, la grille est uniquement affiché en Html. La première chose à faire est donc de créer un fichier Javascript contenant une grille (que vous stockerez comme vous voudrez) dans laquelle vous pourrez mettre des nombres.

Coder ensuite une fonction permettant de modifier la structure Html de la page et d'afficher les nombres présents dans votre grille.

### Placement aléatoire des nombres

Une fois que vous avez trouvé le moyen d'afficher les nombres de votre grille. Vous devrez créer une (ou plusieurs) fonction vous permettant de positionner aléatoirement un nombre dans la grille.

Ce nombre doit aussi être choisi aléatoirement selon ce proportion : 90% de chance d'avoir un 2 et 10% de chance d'avoir un 4.

**Attention #1** : La position aléatoire doit être choisie parmi les cases vides de la grille. Un nouveau nombre doit en aucun cas en écraser un autre !

**Attention #2** : Veillez à faire en sorte de savoir si la grille est pleine et donc ne pas rajouter de nombre dans ce cas.

### Affichage

A tout moment vous pouvez aussi travailler l'aspect visuel de votre 2048. Pour cela, vous devrez utiliser des classes CSS que vous définirez dans un fichier CSS à part.

Ces classes peuvent contenir des animations qui peuvent rendre le jeu plus fun.

Vous êtes libre de choisir les couleurs que vous souhaitez et le thème qui vous plait alors amusez vous !

### Bouton "Nouvelle partie"

Rapidement, vous allez avoir besoin de relancer une partie pour faire des tests.

Créez alors un bouton nouvelle partie qui va tout réinitialiser : la grille, les score etc.

### Détecter les déplacements

Afin de pouvoir jouer à votre jeu, vous allez devoir "écouter" les événements clavier (mais pas que) pour savoir si l'utilisateur à appuyé sur une touche et laquelle.

La syntaxe à utiliser est la suivante :

```js
window.onkeydown = function (event) {
  // Gérer l'événement ici
}
```

Voici la [liste des propriétés](https://developer.mozilla.org/en-US/docs/Web/Events/keydown) de l'événement `keydown`.

Tâchez par exemple de détecter les flèches "haut", "bas", "gauche", "droite" afin de pouvoir en faire quelque chose après.

### Déplacer les nombres dans une direction

Une fois que vous avez la direction choisie par l'utilisateur suite à l'appuis de touche, la prochaine étape consiste à déplacer les nombres dans cette direction, sans les fusionner.

Ex : Si vous avez une ligne avec `2 rien 2 4` et qu'il y a un déplacement à gauche, la ligne deviendra alors `2 2 4 rien`

Peut-être commencez par le faire pour une seule direction dans un premier temps, puis gérer les autres direction après.

Si vous utilisez un `Array` contenant des `Array` représentants les lignes de votre tableau, c'est souvent plus simple de commencer par les déplacement horizontaux ("gauche" et "droite"), plutôt que "haut" et "bas".

Mais tout dépend comment vous avez coder votre 2048...

### Fusionner les nombres

Maintenant que vos nombre vont bien tous dans la même direction, il faut _fusionner_ les nombres égaux.

Attention à ne le faire qu'une seule fois (voir Fonctionnement du jeu) !

C'est une étape pas évidente et c'est peut-être celle qui vous prendra le plus de temps.

A vous de trouver _votre_ méthode, même si ce n'est pas la plus compréhensive, pratique ou élégante, ce qui compte c'est que ce soit là votre.

Pour vous aider, voici un ensemble de cas à traiter si vous allez à gauche (les `0` représentent une case vide) :
* `2, 0, 0, 2` => `4, 0, 0, 0`
* `2, 4, 2, 4` => `2, 4, 2, 4`
* `2, 2, 0, 4` => `4, 4, 0, 0`
* `0, 0, 0, 4` => `4, 0, 0, 0`
* `0, 0, 2, 4` => `2, 4, 0, 0`

### Gérer toutes les directions

Une fois que vous êtes arrivé à fusionner les nombres dans une direction, faites le pour toutes les directions.

_Note : Votre algorithme peut être générique et ne pas nécéssiter de traitement spécifique pour une direction particulière._

### Gérer le game over

Une jeu dois avoir des règles. La règles la plus importante est de savoir quand on à gagner ou perdu.

Gérer ce cas dans le jeu n'est pas forcément évident car il faut anticiper les futurs mouvements et s'assurer qu'il ne peut plus y en avoir même si la grille est pleine.

Je vous laisse chercher comment faire. Encore une fois, même si c'est pas la meilleure solution, essayez :).

### Gérer les scores

L'affichage des scores ne devrait pas être trop un problème. Garder juste une variable que vous mettez à `0` au début de la partie et ajoutez à chaque fusion de nombre réussi le bon score.


## Les commandements de maître Yoda

Votre projet sera aussi bien évalué sur le fond (ce que vous avez fait) que sur la forme (comment vous l'avez fait).

Afin de vous poussez à utiliser des méthodes de travail professionnelles, voici des "commandements" que vous devrez appliquer pour tous les projets Javascript.

### Git tu utiliseras

[git](https://git-scm.com/) logiciel de gestion de version décentralisé. Grosso modo, c'est un outil qui permet aux développeurs de garder un historique des modifications faites dans le code et de pouvoir aisément travailler en équipe.

Il existe plusieurs outils de ce genre mais git est aujourd'hui le plus connu et sans doute le plus utilisé.

Si vous devez apprendre à utiliser un outil pour vous organiser dans votre code, c'est bien celui-ci !

Dans le milieu professionnel, quelques "fous" font encore à l'ancienne et partage du code par FTP, chat ou mail mais cela constitue une très mauvaise pratique.

Garder un historique des modifications et éviter ainsi les pertes de travail suite à des réécritures de fichiers par un tiers est le **B-A-B-A**.

Vous n'allez pas vous contenter de juste utiliser git pour rendre votre travail, vous allez bien l'utiliser et faire des commits réguliers avec des messages qui ont du sens !

Pour cela, des points spécifiques à git sont prévus dans le barême (voir plus bas).

#### Les commandes de base

Voici une petite liste des commandes `git` de base qui vous permettront de créer des commits et rendre votre travail.

##### `git clone`

C'est souvent la commande qu'on utilise quand on commence un projet à partir d'un projet GitHub ou GitLab (voir après) existant.

Elle créer un dossier avec le nom du projet (il est possible de préciser un nom de dossier différent) dans lequel se trouvera les sources du projet ainsi que son historique (contenu dans un dossier caché `.git`).

Sa syntaxe : 

`git clone <adresse_git_du_projet>`

##### `git status`

Permet de savoir dans quel état se trouve son dossier `git`.

Si on veut savoir s'il y a des fichiers modifiés, supprimé, nouveaux, si on diffère du serveur etc.

Cela permet aussi de savoir s'il y a des problèmes (merge ou autre).

Syntaxte :

`git status`

##### `git add`

Vous permet d'ajouter un ou plusieurs fichier au commit que vous êtes en train de créer.

Syntaxe :

`git add <nom_du_fichier>`

Remarque, il est possible d'ajouter plusieurs fichiers à la fois en utilisants des expressions régulières.

Exemple : 

`git add *.js`

##### `git commit`

Une fois que vous avez ajouter tous les fichiers que vous voulez, vous pouvez créer un _commit_.

Il s'agit de mettre un message sur un ensemble de modifications.

Plus le commit est petit et plus le message de commit est précis, mieux c'est !

N'hésitez pas à faire plusieurs commits par jour !

Dès que vous faites une petite modification dans votre code, faites un commit, il n'y en a jamais trop (enfin faut pas abuser non plus).

Il est fortement conseillé d'écrire vos messages de commit en **anglais** !

_Note : J'utilise l'option `-m` pour préciser le message de commit directement sur la ligne de commande. Si vous avez beaucoup de choses à dire, ne l'utilisez pas, un éditeur de texte s'affichera et vous pourrez mettre autant de texte que vous voudrez._

Ex :

`git commit -m "Add CSS classes on the grid"`

Evitez les messages trop évasifs genre :

`git commit -m "Update code"` ou `git commit -m "Fix bug"`

Tâchez de préciser au moins le nom du fichier impacté ou s'il y en a plusieurs, la fonctionnalité.

Encore une fois, tâcher de séparer au maximum les commits. Pensez fonctionnalités !

###### Changer le dernier commit

Il est assez simple de changer le dernier commit en utilisant l'option :

`git commit --amend`

Au lieu de créer un nouveau commit, `git` ajoutera les nouvelles modifications au commit précédent et vous permettra de modifier le message.

Pratique quand on s'est trompé ! Par contre, attention quand on travail à plusieurs car le commit change de _hash_.

##### `git checkout`

C'est une commande qui peut être utilisée dans plusieurs cas (changement de branche notamment) mais là on va l'utilser pour annuler des modifications sur un fichier.

Si vous avez modifié un fichier, **sans l'avoir ajouté au commit**, mais que finalement vous voulez **revenir à sa version initiale** (celle du dernier commit) vous pouvez faire :

`git checkout <nom_du_fichier>`

Si vous voulez annulé l'ajout d'un fichier au commit courant, il faudra utiliser la commande `git reset` décrire juste après.

##### `git reset`

Parfois, on veut tout annuler, revenir à la version initiale d'un projet, `git reset` est fait pour ça.

**Attention la commande qui suite réinitialise tout le projet par rapport à une version précise. Toutes les modifications faites ultérieurement seront perdues**

`git reset --hard <nom_de_la_branche_ou_du_commit_ou_du_depot_distant>`

Quand on a modifié un fichier et qu'on l'a déjà ajouter au commit courant, si on veut annuler l'ajout au commit (le "désindexé"), il faut faire un :

`git reset HEAD <nom_du_fichier>`

Il ne vous restera plus qu'à faire un `git checkout <nom_du_fichier>` pour annuler vos modification.


##### `git log`

Cette commande vous montre l'ensemble des commits d'une branche avec leur hash et les messages.

Très pratique quand on veut voir l'historique d'un projet.

`git log`

##### `git show`

Permet de voir le détail d'un commit qu'on a vu dans les logs.

`git show <hash_du_commit>`

##### `git pull`

Cette commande vous permet de récupérer les dernières modifications effectuées sur le dépôt distant.

Si vous avez fait des modifications sur votre dépôt local, il faudra alors _merger_ les deux dépôts et cela donne souvent la création d'un _commit de merge_.

Syntaxe :

`git pull <nom_du_depot_distant> <nom_de_la_branche>`

Ex : 

`git pull origin master`

Parfois, `git` ne peut pas merger automatiquement les sources, c'est souvent le cas quand vous avez modifier un fichier qui a aussi été modifié dans le dépôt distant.

Dans ce cas là, il faut faire le merge manuellement et c'est une autre pair de manche !

Je vous conseille pour cela d'utiliser des outils comme `meld`

`sudo apt install meld`

Ensuite configurer git pour qu'il utilise `meld` :

`git config --global merge.tool meld`

Puis, vous pouvez faire un `git merge` après.

Je vous conseille de vous faire aider par quelqu'un d'expérimenté les premières fois.

##### `git push`

Une fois que vous aurez fait vos commits, récupéré les dernières sources du serveur, gérer les éventuels conflits, vous pourrez publiez vos modification sur le dépôt distant !

Syntaxe :

`git push <nom_du_depot_distant> <nom_de_la_branche>`

Ex : 

`git push origin master`


##### Et d'autres encore

Il existe beaucoup d'autres fonctions `git`, on a peu parlé des dépôts distants et des branches, mais ça sera pour plus tard !

Avec ces quelques commandes, vous devrez déjà être plus ou moins autonome :).

### Sur Gitlab ton projet tu rendras

Si `git` est aussi connu c'est en grande partie grace au site [github](github.com), sorte de facebook pour développeurs open source.

Ce site a _radicalement_ changer la manière dont on fait du code. Que ce soit au niveau de la documentation, des commits, de la gestion de bugs, de la participation à un projet etc. Tout à changer !

Et en bien mieux ! Grâce à Github, il est aujourd'hui beaucoup plus facile de participer au développement communautaire d'un logiciel.

De plus, Github a instauré une sorte de "standard" qui profite à l'ensemble des développeurs.

C'est donc un site génial dont le seul défaut et de ne pas être basé sur un [logiciel libre](https://fr.wikipedia.org/wiki/Logiciel_libre).

C'est pour cela que le projet [GitLab](https://about.gitlab.com/) a vu le jour et c'est pour cela qu'on utilisera pour notre projet une instance de Gitlab hébergée gracieusement par l'excellente association [framasoft](https://framasoft.org).

Pour cela faites les étapes suivantes :

* Créez-vous un compte sur [framagit](www.framagit.org)
* Ensuite "forker" ce projet en cliquant sur le lien "fork" sur la page d'accueil du projet
* Cela va faire une copie du projet dans votre espace personnel
* Vous n'avez plus qu'à cloner le projet sur votre disque dur avec l'adresse fournit par framagit :
* Ex : `git clone git@framagit.org:<votre_nom>/2048-lafabrique.git`

Puis pour rendre votre projet vous n'aurez qu'à faire un `git push` comme décrit plus haut.

### Formater ton code tu dois

S'il y a bien quelque chose qui fait débat parmis les développeurs, c'est la forme que dois prendre notre code.

Il faut dire qu'il est très embêttant de lire du code mal formaté (par exemple sans tabulation) et on peut être perturbé par lire du code qui ne suit pas les mêmes règles de formatage.

Afin de clore le débat une bonne fois pour toute, certains langage géniaux comme [go](golang.org) ou encore [elm](http://elm-lang.org/) incluent un outil de formattage automatique du code que tout le monde applique.

Il n'y a donc plus qu'une seule manière d'écrire du code, finit les débat interminables et assez stérils !

[Un outil similaire](https://prettier.io/) à été mis au point pour Javascript et vous devrez l'utiliser pour ce projet (en tout cas votre code devra être formater de la même manière).

Il s'agit de [prettier](https://prettier.io/).

Je vous invite dès maintenant à l'installer globalement avec `npm`:

`npm install -g prettier`

Puis d'installer un plugin pour l'intégrer automatiquement à votre éditeur de texte préféré. Vous trouverez les listes des plugins existants dans la partie "Editor integration" de la page d'accueil du site.

Pour s'assurez que tout fonctionne bien, créer un fichier Javascript, dans lequel vous mettez du code valide mais écrit n'importe comment, par exemple le code se trouvant [sur cette page à gauche](https://prettier.io/playground/), et votre code devrait être transformé en quelque chose de beaucoup plus lisible.

Si ce n'est pas le cas, c'est qu'il y a un souci, cherchez pourquoi et demander de l'aide si le problème persiste.

### Eslint ton code valide sera

Javascript étant un langage non typé et par défaut assez permissif, il est possible de faire beaucoup d'erreurs sans en être averti.

C'est pratique quand on bidouille un petit site dans son coin car on a rapidement quelque chose même si on code avec les pieds, par contre, dès que l'on commence à travailler à plusieurs sur des applications web de plusieurs milliers de lignes, là ça devient compliqué !

C'est pour ça qu'on rapidement émergé des outils appelés _linter_ qui font des vérifications de votre code et vous avertissent lorsqu'il y a un problème potentiel.

[eslint](eslint.org) est le plus connu d'entre eux pour javascript et c'est celui que nous allons utiliser pour notre projet.

Pour des raisons pratiques, on va aussi l'installer globalement :

`npm install -g eslint`

Eslint fonctionne avec un fichier de configuration : `.eslintrc.json` (ou .js, .yaml). Il précise le comportement du linter, quels sont les règles à utiliser etc.

Un fichier de ce genre est déjà écrit pour le projet 2048, vous n'avez donc plus qu'à appeler eslint sur vos fichiers pour vérifier qu'ils sont bien conformes.

`eslint <nom_du_fichier>`

Vous pouvez aussi [intégrer `eslint` avec votre éditeur de texte préféré](https://eslint.org/docs/user-guide/integrations), c'est assez pratique :

Tout code rendu devra généré aucune erreur et aucun warning eslint ! 

### Bryan is in the kitchen

L'anglais est **LA** langue à utiliser quand on programme. C'est peut-être embêttant mais c'est comme ça. Cela permet à n'importe qui de lire votre code et de le comprendre.

Vous devrez donc nommer vos variables et vos fonctions en anglais.

Seule exception à la règles : si votre application traite de choses spécifique à une région ou une langue et qu'il n'y a pas de traduction valable.

Pour m'aider dans le choix des mots, j'utilise très régulièrement l'excellent [WordReference](http://www.wordreference.com/) qui donne plusieurs traductions en fonction du contexte, ce qui est bien plus utile qu'un simple google translate.

### Small is beautifull

Derrière cette phrase se cache un élément essentiel en programmation : **ne faites pas des fonctions ou des fichiers trop gros.**

Généralement, si une fonction est trop longue, c'est qu'elle fait plusieurs choses et que normalement, une fonction ne devrait faire qu'une et une seule chose.

C'est difficile au début de comprendre cette règle et de l'appliquer, mais vous serez aussi noté là dessus, alors attention !

### Jamais tu ne copieras

Vous êtes là pour apprendre, pas pour avoir à tout prix une bonne note. Ce qui compte dans ce projet, ce n'est pas de le finir (ça serait super si vous y arrivez) mais surtout le processus de recherche et d'apprentissage que vous avez mis en oeuvre.

Il sera très évident pour moi de voir si vous avez pris du code sur internet ou sur vos camarades. Surtout que vous ne serez certainement pas en mesure de l'expliquer.

Si jamais une triche devait être découverte, vous serez sanctionné par une mauvaise note et l'équipe pédagogique sera avertie.

Cela ne veut pas dire que vous ne pouvez pas discuter entre vous, ou vous inspirer de choses que d'autres ont fait, c'est le principe d'internet et des logiciels libres, juste que vous devez comprendre tout ce que vous écrivez.

### Du javascript récent tu utiliseras

Nous n'avons pas le temps de voir toute l'histoire de javascript, mais c'est un langage qui a beaucoup évolué ces dernières années.

De nouveaux mots clés sont arrivés et de nouvelles manières de faire beaucoup plus propres. Vous devrez donc n'utiliser que les dernières fonctionnalités du langage.

Pour cela, Eslint a été configurer pour vous guider et levera des _warnings_ quand vous n'utilisez pas une fonctionnalité ES6 (ou ECMAScript2015, nom de la dernière version majeur de Javascript).

Ex. en ancien javascript (comme en ancien français sauf que c'était il y a juste quelques années :) on écrivait pour déclarer une variable :
```js
var maVar = 10;
```

En javascript ES6, il faut maintenant utiliser le mot clé `let` ou `const` :
```js
const maVar = 10; // Si on ne veut pas réaffecter la variable
let autreVar = 12; // Si on veut réaffecter la variable
autreVar = 14;
```

## Barème

Comme annoncé plus haut, le barême prendra aussi bien en compte le fond (est-ce que votre jeu fonctionne) que la forme (est-ce que vous avez respéctez les différentes consignes, est-ce que le jeu est "beau" etc.).

Voici une liste des points qui seront évalués lors de la soutenance.

Si votre projet répond à tous les critères, vous aurez la note maximale.

Pour éviter que vous ne fassiez qu'une "chasse aux points", je ne précise pas le nombre de points de chaque éléments, sachez juste que ça sera équitablement réparti en fonction de la difficulté de chaque tâche.

### Forme

#### Rendu à temps

La date buttoire de rendu du projet est le dimanche **1er avril (on pouvait pas rêver mieux!) à 22h22** petante !
Non seulement, les commits effectués après ne seront pas pris en compte mais vous devrez avoir _pusher_ vos modification sur votre projet gitlab avant cette heure-ci.

Et pas question de me dire qu'il y a eu un souci technique à 21h50, à vous de vous assurez que tout fonctionne bien avant. Rappelez-vous, vous pouvez faire plusieurs commits.

Je récupérerai donc à cette heure là tous les projets sur gitlab en faisant un bête :
`git pull origin master`

#### Rendu dans les bonnes modalités

Vous devez non seulement rendre à temps, mais sur un dépôt gitlab comme précisé plus haut. La branche utilisée doit être `master` (rien à faire normalement, c'est le fonctionnement pas défaut).

Normalement ça doit être _easy_ :).

#### Plusieurs commits avec messages explicites

Un `git log` sur votre projet doit afficher au moins 10 commits avec des messages **en anglais** et explicites comme je l'ai expliqué plus haut.

Si ce n'est pas le cas, vous n'aurez pas tous les points pour ce critère.

#### Code écrit dans un anglais compréhensible

Vos noms de variables et vos noms de fonctions devront être en anglais et ne pas être de grosses abréviations ou ne pas avoir de signification (ex : `let a = 0;`).

A vous de vous assurez avant la date buttoire que vos noms sont bien choisis en faisant lire votre code par vos camarades par exemple.

#### Fonctions pas trop grosses

Comme précisé plus haut aussi, vos fonctions ne devront pas être trop importantes.

#### Pas de duplication de code

Quand on débute, on a souvent tendance à copier/coller son code un peu partout et ça devient vite n'importe quoi. Si je vois du code qui se ressemble trop, vous serez sanctionné.

L'idée est de faire des fonctions génériques qui permettent de réutiliser plusieurs fois une même logique de code.

#### Eslint OK

Je dois pouvoir passer eslint avec le fichier `.eslintrc.json` sans aucune erreur, ni warning.

#### Code formaté

Votre code doit être formaté avec prettier ayant les réglages par défaut.

#### Module ES6

Tout votre code javascript doit se trouver dans des modules ES6. Il est interdit d'écrire du code js dans une balise `<script></script>` de votre html.

### Fond

#### Position aléatoire des 2 premiers nombres

#### Déplacement des tuiles avec les touches au moins dans une direction

#### Fusion des nombres fonctionnelle au moins dans une direction

#### Apparition d'une nouvelle tuile après un déplacement

#### Gestion du game over

#### Message quand on a gagné

#### Déplacement fonctionnel dans toutes les directions

#### Fusion des nombres fonctionnelle dans toutes les directions

#### Jeu "joli" et original

#### Utilisation des bonnes classes CSS

#### Bonus

##### Sauvegarde des meilleurs scores

##### Sauvegarde de la partie en cours

##### Animation sur les déplacements

##### Animation pour les nouvelles tuiles

##### Gestion des événements touch

