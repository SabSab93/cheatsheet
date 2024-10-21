# Introduction à git


Git est un logiciel 
Origin github gitlab gitserver ce sont des origins c’est un onedrive
Code CI/CD devops permet de faire des test 
Github permet de mettre nos travaux accesible à tous 
open source

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
- Donnez un nom au dépôt, ajoutez une description si nécessaire, visibilité : public ou privé (ne pas hesiter à mettre les travaux en public), et cliquez sur "Create repository".
- Une fois le repository creer, git nous facilite en indiquant les commandes à taper dans notre terminal afin de connecter notre projet local à l'origin :

![Create repository cde](/image/GitPart/create_new_repo_or_push.png "Commande à taper lors d'une creation repo")

:bulb: A savoir

Nous pouvons modifier les parametres de notre repo à tout moment dans la rubrique "setting"
-   Renommer le repository
-   Modifier le nom de la branche principale "main" (_cf : Historiquement, la branche principale d'un dépôt Git était souvent nommée master, mais de plus en plus de projets utilisent main pour des raisons de neutralité et d'inclusivité suite à l'affaire George Floyd._)
-   De changer la visibilité (privé/public)/ de supprimer... dans la partie "Danger Zone"


#### 1er cas : Creation d'un nouveau repository :

``` git
cd chemin/vers/votre/projet
```
Ces commandes doivent etre saisie dans le repertoire du projet
****

```git
echo "# Repo_Test" >> README.md 
```
Ajouter une ligne de texte à un fichier nommé README.md - Facultative 
****

```git
git init
```
Initialiser un dépôt Git; Git crée un sous-répertoire caché nommé .git. Ce répertoire contient tous les fichiers et dossiers nécessaires pour gérer le dépôt Git.  - Important et obligatoire
****

```git
git add README.md
```
Ajouter le fichier README.md à l'index de Git - Facultative mais crucial, le README.md sert de point d'entrée pour les utilisateurs qui visitent notre dépôt et fournit des informations essentielles sur notre projet : 
Présentation du Projet /  Instructions d'Installation / Guide d'Utilisation / Contribution / Licence / Documentation ...
****

```git
git commit -m "first commit"
```
Est utilisée pour enregistrer les modifications ajoutées à la staging area. 

commit : est une capture instantanée de l'état de votre projet à un moment donné
message du commit : l'option -m permet de spécifier le message de commit directement dans la commande ici : first commit

_Avoir le reflex de commit les travaux le plus souvent possible !_
****

```git
git branch -M main
```
Est utilisée pour renommer la branche actuelle en "main".

git branch : La commande git branch est utilisée pour gérer les branches dans un dépôt Git. Elle permet de créer, lister, renommer et supprimer des branches. 

L'option -M est utilisée pour renommer une branche. Si on utilise -m (en minuscule), Git renommera la branche uniquement si le nouveau nom n'existe pas déjà. L'option -M (en majuscule) forcera le renommage même si le nouveau nom existe déjà.
****


```git
git remote add origin git@github.com:SabSab93/Repo_Test.git
```
Est utilisée pour ajouter un dépôt distant au dépôt local Git

git remote : La commande git remote est utilisée pour gérer les dépôts distants. Elle permet d'ajouter, de lister, de renommer et de supprimer des dépôts distants.

origin : origin est le nom par défaut donné au dépôt distant. C'est une convention couramment utilisée.

git@github.com:SabSab93/Repo_Test.git : C'est l'URL du dépôt distant sur GitHub. Cette URL utilise le protocole SSH pour accéder au dépôt.
****
```git
git push -u origin main
```
Permet de pousser les modifications vers le dépôt distant :
****

#### 2ème cas : Pousser un repository existant 

Des commandes en moins (bien penser à creet le .git)
```git
git remote add origin git@github.com:SabSab93/Repo_Test.git
git branch -M main
git push -u origin main
```











Les commandes essentielles
On créé un fichier qui contiendra notre projet et dans ce dossier nous creeons :
- git init : initialiser notre repo (repertoire) avoir un .git dans le dossier. Premiere chose à faire initialiser le git en ajouter git init


- git clone : récupérer le repo git de quelqu’un exemple : git clone « lien du repo ex dans github » « nom de dossier a renommer »
- git status : pour voir les status
- git diff :permet d’ouvrir la vue des diff dans le code entre avant après, ce sont la vu des modifications, il ouvre une autre page 
- git log : affiche tous les commit avec le user et la date pour sortir « :q »


- git add :tous les fichiers que j’ajoute dans mon git c’est un stage changes ce n’est pas réversible on peut repartir en arrière



    - Possibilité de definir des rôles dans le cas où il y a une collobaration dans : Rules / Rulests: nous pouvons cocher 
        - restrict deletions
        - require linear history
        - require deployments to succeed 
        - require a pull request befoore merging
            - require approvals 1
            - require review from code Owners
            - dismiss state pull request approvals when new commits are pushed
        - require statuts cheks to pass
        - block force pushes



SSH
