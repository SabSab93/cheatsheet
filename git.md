# Introduction à git


Git est un logiciel 
Origin github gitlab gitserver ce sont des origins c’est un onedrive
Code CI/CD devops permet de faire des test 
Github permet de mettre nos travaux accesible à tous 


Il existe la doc officielle https://git-scm.com/


# Manipulation git

Afin de travailler avec git nous pouvons suivre les étapes suivantes. Nous pouvons soit creer un nouveau projet, soit cloner afin de travailler en collaboration.
Avant tout nous devons creer un compte et installer le logiciel git.

## Créer un compte GitHub
Creer un compte sur github.com et parametrer votre compte git avec une double autentification.

## Installer Git
Git doit etre installé sur notre machine. On peut le télécharger depuis git-scm.com.

## Creer un nouveau projet 

### Configurer Git
Ouvrir le terminal wsl et configurez Git avec le nom d'utilisateur et l'adresse e-mail utilisée sur github (manipulation à réaliser une seule fois) :

```git
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

### Créer un dépôt (repository) sur GitHub

- Se rendre sur notre GitHub.
- Cliquez sur le bouton "+" en haut à droite et sélectionnez "New repository".
- Donnez un nom au dépôt, ajoutez une description si nécessaire, et cliquez sur "Create repository".
- Nous pouvons modifier les parametres de notre repo à tout moment dans la rubrique "setting"
    -   Renommer le repository
    -   Modifier le nom de la branche principal "main" (_cf : depuis l'affaire George Floyd modification de la branche principale master en main._)


### Initialiser un dépôt Git local
Se rendre dans le répertoire de notre projet dans le terminal ou bien dans VS code et initialisez un dépôt Git :

```git
cd chemin/vers/votre/projet
git init
```

Les commandes essentielles
On créé un fichier qui contiendra notre projet et dans ce dossier nous creeons :
- git init : initialiser notre repo (repertoire) avoir un .git dans le dossier. Premiere chose à faire initialiser le git en ajouter git init


- git clone : récupérer le repo git de quelqu’un exemple : git clone « lien du repo ex dans github » « nom de dossier a renommer »
- git status : pour voir les status
- git diff :permet d’ouvrir la vue des diff dans le code entre avant après, ce sont la vu des modifications, il ouvre une autre page 
- git log : affiche tous les commit avec le user et la date pour sortir « :q »


- git add :tous les fichiers que j’ajoute dans mon git c’est un stage changes ce n’est pas réversible on peut repartir en arrière
