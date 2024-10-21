# Introduction à git


Git est un système de contrôle de version distribué **open source**, largement utilisé pour le développement de logiciels. Il a été créé par Linus Torvalds en 2005 pour gérer le développement du **noyau Linux**. C'est un logiciel qui peut être utilisé et heberger par different Git server tel que **GitHub** ou  **GitLab**.


Il existe la doc officielle : https://git-scm.com/


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

git@github.com:SabSab93/Repo_Test.git : C'est l'URL du dépôt distant sur GitHub. Cette URL utilise le protocole **SSH** pour accéder au dépôt.

```git
git push -u origin main
```
Permet de pousser les modifications vers le dépôt distant (origin).
****

#### 2ème cas : Pousser un repository existant 

Des commandes en moins (bien penser à creet le .git)
```git
git remote add origin git@github.com:SabSab93/Repo_Test.git
git branch -M main
git push -u origin main
```

## Travailler sur un depôt existant 

### Cloner un dépot existant 
Possibilité de recuperer un projet d'un autre collaborateur git et de travailler en collobaration.
- Pour cela nous devons recuperer le code grâce à la clé **SSH**. Dans le depôt se rendre dans <>code: copier URL de la clé SSH : <URL du dépôt en SSH>
- Se rendre dans le terminal et taper :

```git
git clone <URL du dépôt en SSH> [nom du répertoire local]
```
git clone : est utilisée pour créer une copie locale d'un dépôt distant. Cette commande permet de télécharger l'intégralité du dépôt, y compris son historique de commits, ses branches, et ses tags, sur notre machine locale.

[nom du répertoire local] : c'est optionnel, on renome le nom du répertoire dans lequel le dépôt sera cloné. Par defaut c'est le nom du dépot d'origin.

### Travailler en collaboration
A partir de là, nous pouvons travailler sur ce projet copié. Nous pouvions travailler en collobaration afin de partager le travail et de d'avancer le projet simultanément.

Sur settings 
-   Dans Access/Collaborators :
    -   Accepter l'invitation ou Add people pour ajouter un/des collaborateurs
-   Dans branches : on redifnit les roles 
    -   Add branch ruleset, cocher les elements ci-desous :
        - restrict deletions
        - require linear history
        - require deployments to succeed 
        - require a pull request before merging
            - require approvals 1
            - require review from code Owners
            - dismiss state pull request approvals when new commits are pushed
        - require statuts cheks to pass
        - block force pushes


****
<h1 align="center">Definitions</h1>

Noyau Linux : lE composant central du système d'exploitation Linux. Il joue un rôle crucial en gérant les ressources matérielles et en fournissant une interface entre le matériel et les logiciels.
****
Open Source : Le noyau Linux est un logiciel open source, ce qui signifie que son code source est disponible gratuitement et peut être modifié, distribué et utilisé par n'importe qui. Cette nature open source a permis une collaboration mondiale et une amélioration continue du noyau.
****
Git Server : Un serveur qui héberge des dépôts Git, pouvant être configuré et géré par une organisation ou un individu. Exemple : GitHub et GitLab sont des exemples de services de serveurs Git hébergés.
****
GitHub : Plateforme de collaboration basée sur Git. Elle offre une interface web pour héberger des dépôts Git, permettant aux développeurs de collaborer sur des projets, de suivre les modifications, de gérer les versions, et de discuter des problèmes et des améliorations.
****
GitLab : Une autre plateforme de collaboration basée sur Git, offrant des fonctionnalités similaires à GitHub, avec un accent sur l'intégration continue et la livraison continue; à utilisation profesionnelle.
****
SSH : Un protocole qui permet de se connecter à des serveurs distants de manière sécurisée. Il utilise le chiffrement pour protéger les données transmises et pour authentifier les utilisateurs.
****
Clé SSH : Une paire de clés cryptographiques utilisée pour authentifier les utilisateurs. La paire de clés comprend une clé publique et une clé privée.

- Clé publique : Cette clé est partagée avec le serveur (par exemple, GitHub) et est utilisée pour chiffrer les données.
- Clé privée : Cette clé reste sur votre machine locale et est utilisée pour déchiffrer les données. Elle doit être gardée secrète et sécurisée.
****