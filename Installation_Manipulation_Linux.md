# Installation et manipulation des commandes sous Linux

## Introduction

Possibilite de travailler sous macOs, Windows ou Linux.

Il est preferable de travailler sous le systeme d'exploitation <span style="color:red"> Linux</span> . Il existe d'autres possibilités (Installer Linux ou double boot càd avoir 2 systemes) 

Dire les avantages de Linux comparer aux autres.

## Installation

Et pour ce faire, nous devons configurer notre pc afin de creer un sous syteme.
Linux est un <span style="color:red"> système d’exploitation</span> de type <span style="color:red">Unix</span> basé sur le <span style="color:red"> **noyau Linux**</span>.


Afin de travailler sous Linux, il faut virtualiser Windows et ajouter les fonctionnalités du Sous-système Windows pour Linux (wsl) dans  "Activer ou désactiver des fonctionnalités Windows" dans les parametres windows.

Cocher :
- Sous-systemes Windows pour Linux
- Plateforme de l'hyperviseur Windows

Redemarrer le pc


Installer la distribution ubuntu dans Microsoft Store et le lancer.

Ouvrir le terminal WSL.

## Les commandes sous Linux

Une fois l'installation réalisée, nous avons manipulé quelques commandes afin de nous familiariser avec le terminal. Ci-dessous les commandes utilisées :

****
``` batch
apt – get 
```
L'outil de gestion de paquet.  Elle permet d'installer (install), de mettre à jour (update or upgrade), de supprimer (remove) et de gérer des paquets logiciels. 
``` batch
apt – get install nom-du-paquet-a-installer
```
****


``` batch
touch nom-du-fichier.type
```
Pour créer des fichiers vides
****


``` batch
mkdir nom-du-répertoire
```
Créer un ou plusieurs répertoires spécifiés. 
****


``` batch
cd [options] [répertoire]
```
Change directory est utilisée pour changer le répertoire de travail courant dans le terminal. Elle permet de naviguer dans la structure de répertoires du système de fichiers. 

options : 
-   "-" : Permet de revenir au répertoire précédent. C'est une manière rapide de basculer entre deux répertoires.
-   "~" : Représente le répertoire personnel (home directory) de l'utilisateur. Par exemple, cd ~ change le répertoire de travail pour le répertoire personnel de l'utilisateur.
-   ".." :Représente le répertoire parent. Par exemple, cd .. change le répertoire de travail pour le répertoire parent du répertoire courant.
****


``` batch
ls [options] [répertoire (parametre factultatif)]
```
Afficher une liste des fichiers et des répertoires dans le répertoire courant ou dans un répertoire spécifié
options :
- "-a" : Affiche tous les fichiers, y compris les fichiers cachés (ceux dont le nom commence par un point . ex: .git)
- "-l" : Affiche les fichiers et les répertoires en format long, incluant les permissions, le nombre de liens, le propriétaire, le groupe, la taille, et la date de modification.
****


``` batch
pwd 
```
Affiche le chemin du répertoire de travail courant.
****


``` batch
 mv source destination
```
Déplacer ou renommer des fichiers et des répertoires.

Exemples :
``` batch
mv fichier_source.txt /chemin/vers/destination/  --> Cette commande déplace fichier dans un repertoire
mv fichier_source.txt fichier_destination.txt --> Cette commande renomme source à destination
mv repertoire_source/ /chemin/vers/destination/ --> Deplacer le répertoire source à destination
mv fichier1.txt fichier2.txt /chemin/vers/destination/ --> Déplacer plusieurs fichiers 
```
****


``` batch
 cp [options] source destination
```
Copier des fichiers et des répertoires d'un emplacement à un autre.

-r ou -R : Copie les répertoires de manière récursive, c'est-à-dire en incluant tous les sous-répertoires et leurs contenus.

Exemple : 
``` batch
cp fichier_source.txt fichier_destination.txt --> Copier un fichier
cp fichier_source.txt /chemin/vers/destination/ --> Copier un fichier dans un répertoire 
cp -r repertoire_source/ repertoire_destination/ --> Copier un répertoire de manière récursive copie le répertoire /source et tous ses sous-répertoires et fichiers dans /destination
cp fichier1.txt fichier2.txt /chemin/vers/destination/ --> Copier plusieurs fichiers :
```
****


``` batch
rm [options] fichier(s)
 ```
Est utilisée pour supprimer des fichiers et des répertoires.

-r ou -R :Supprime les répertoires et leur contenu de manière récursive. 
****


``` batch
 cat
```
Affiche le contenu de fichiers. Elle est couramment utilisée pour lire et afficher le contenu de fichiers texte dans le terminal
****


Les alias : On peut créer des raccourcis de commandes Les alias permettent de simplifier et de personnaliser l'utilisation des commandes dans le terminal. Dans le dossier ~/.bashrc.
``` batch
alias ll='ls -l'
 ```
****

<h1 align="center">Definitions</h1>

 Systeme d'exploitation : Logiciel système qui gère les ressources matérielles et logicielles d'un ordinateur. Il fournit une interface entre l'utilisateur et le matériel, permettant aux utilisateurs d'exécuter des applications et de gérer les ressources de manière efficace. Le système d'exploitation est responsable de la gestion des processus, de la mémoire, des périphériques d'entrée/sortie, des systèmes de fichiers, et de la sécurité. Exemples : Windows, macOS,...
****
 UNIX : est un système d'exploitation conçu pour être portable, multitâche et multi-utilisateur. Il a été développé pour fournir un environnement stable et efficace pour le développement de logiciels et la gestion des ressources matérielles.
 
 Il fournit une interface utilisateur, qui peut être en ligne de commande (CLI) ou graphique (GUI). L'interface utilisateur permet aux utilisateurs d'interagir avec le système et d'exécuter des applications.

 ****
 Linux :  Un système d'exploitation open source basé sur Unix, largement utilisé sur une variété de dispositifs, des ordinateurs personnels aux serveurs et aux appareils embarqués.



