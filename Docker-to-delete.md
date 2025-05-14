# Docker

## Rendu

Un tp qui retrace tout le cours + une evaluation écrite
Mettre en place le docker dans le projet.

## Introduction

Docker est une plateforme open source permettant d'unifier l'environnement de prod. 
cela permet de creer des conteneurs = à une image virtuelle. 

- Flexible : toute app peut etre transformée en conteneur
- Leger: ressources de la amchine hote
- Portable : son ordinateur, celui de ses clients ou un serveur distant
- Auto-suffisant : L'installation et la desinstallation de conteneur ne depend pas des autres conteneyrs installés
- Scalable : scalabilité horizontale aisement
- securisé: isole les processus
- auto documenté ; dockerfile suffisant pour decrire l'application et ses dependances : grâce à dockerfile

## Structure d'un Dockerfile

FROM :image de base :  C'est toujours la première instruction. Elle spécifie l'image de base à partir de laquelle nous construisons. Cela crée la première couche de notre image, qui inclut le runtime Python. dockerhub avec alpine : https://hub.docker.com/ alpine car legere il faudra justifier le choix de l'image 

WORKDIR/app : la ou tout se passe  Cela définit le répertoire de travail pour les instructions suivantes. Elle ne crée pas une nouvelle couche, mais affecte le comportement des instructions suivantes.

COPY : copie des fichiers Cela copie le fichier de dépendances de notre hôte dans l'image. Cela crée une nouvelle couche contenant uniquement ce fichier.

RUN : commande à lancer Cela exécute une commande dans le conteneur pendant le processus de construction. Elle installe nos dépendances Python. Cela crée une nouvelle couche qui contient tous les packages installés.

EXPOSE: port à exposer En réalité, il s'agit simplement d'une forme de documentation. Elle indique à Docker que le conteneur écoutera sur ce port à l'exécution, mais ne publie pas réellement le port. Elle ne crée pas de couche.

CMD : commande à lancer au demarrage  Cela spécifie la commande à exécuter lorsque le conteneur démarre. Elle ne crée pas de couche, mais définit la commande par défaut pour le conteneur.

## Et apres ?

### .dockerignore

### Construire l'image

``` 
docker build . -t <your username>/mon-app
``` 
### Demarrer l'image

 ```
 docker run -p 49160:8080 -d <your username>/node-web-app
 ```

Difference d'une image et d'un conteneur 


### Lancer la ligne de commandes deans le conteneur

la parte de droite :80 est l'image docker

https://blog.stephane-robert.info/docs/conteneurs/moteurs-conteneurs/docker/cheat-sheet/

https://kinsta.com/fr/blog/commandes-docker/


### Qu'est ce que Docker compose ? 

Docker compose est un outil qui permet de décrire et lancer plusieurs conteneurs en meme temps

- Il permet de decrire les relations entre les contenerus
- Il permet de decrire les variable d'environnement des differents conteneurs
- Il permet de décrire les volumes partagés entrtes les conteneurs
- Il permet de décrire les ports exposés par les conteneurs


### Comment utiliser un docker compose ?

docker-compose up -d : permey de demarrer l'ensemble des conteneurs en arriere plan
docker-compose ps : permey de voir le statut de l'ensemble de votre stack
docker-compose logs -f --tail 5 : permey d'afficher les logs de votre stack les 5 derniers logs...
docker-compose stop
docker-compose down

docker-compose config : permet de valider la syntaxe 

important :  interet du micro service avec un petit api, gerable 


difference entre CI et CD; il y a des zones intermediaires



