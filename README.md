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
    * Lors de ce décalement, si 2 nombres identiques se retrouvent côte à côte, ils sont alors "fusionné" en un seul nombre qui prend la place du nombre le plus loin dans la direction de la grille.
    * Un nouveau nombre est généré aléatoire même si aucun nombre ne bouge après un décalement (ie ils étaient déjà tous décaler dans la direction)
    * Un nombre "fusionné" prend comme valeur **la somme des deux des nombres.**
    * Cette valeur s'ajoute alors au score de la partie. Ex: on fusionne deux nombres 4, ce qui donne un chiffre fusionné 8 et ajoute ainsi 8 au score.
    * Attention, un chiffre "fusionné", ne peut pas se fusionner à nouveau dans le même déplacement !
    * Exemple : si sur une ligne il y a : "2 rien 2 4", lors d'un déplacement à droite, la ligne deviendra : "rien rien 4 4"
    * Après chaque déplacement, un nouveau chiffre apparait aléatoirement aux endroits vides de la grille selon les mêmes modalités que le chiffre de départ (90% de chance de 2 et 10% de 4).
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



### Small is beautifull

### Jamais tu ne copieras

### Du javascript récent tu utiliseras