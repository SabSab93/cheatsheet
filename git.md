# Introduction à git


Git est un logiciel 
Origin github gitlab gitserver ce sont des origins c’est un onedrive
Code CI/CD devops permet de faire des test 
Github permet de mettre nos travaux accesible à tous 


Il existe la doc officielle https://git-scm.com/


# Manipulation git

Afin de travailler avec git nous devons suivre les étapes suivantes :


## Créer un compte GitHub
Creer un compte sur github.com

## Installer Git
Git doit etre installé sur notre machine. On peut le télécharger depuis git-scm.com.

## Configurer Git
Ouvrir le terminal wsl et configurez Git avec le nom d'utilisateur et l'adresse e-mail utilisée sur github (manipulation à réaliser une seule fois) :

```git
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

## Créer un dépôt (repository) sur GitHub

- Se rendre sur notre GitHub.
- Cliquez sur le bouton "+" en haut à droite et sélectionnez "New repository".
- Donnez un nom au dépôt, ajoutez une description si nécessaire, et cliquez sur "Create repository".



Les commandes essentielles
On créé un fichier qui contiendra notre projet et dans ce dossier nous creeons :
- git init : initialiser notre repo (repertoire) avoir un .git dans le dossier. Premiere chose à faire initialiser le git en ajouter git init


- git clone : récupérer le repo git de quelqu’un exemple : git clone « lien du repo ex dans github » « nom de dossier a renommer »
- git status : pour voir les status
- git diff :permet d’ouvrir la vue des diff dans le code entre avant après, ce sont la vu des modifications, il ouvre une autre page 
- git log : affiche tous les commit avec le user et la date pour sortir « :q »


- git add :tous les fichiers que j’ajoute dans mon git c’est un stage changes ce n’est pas réversible on peut repartir en arrière
