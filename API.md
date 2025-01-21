# API

Utilisation de la stack nodeJS pour le backend, en continuité avec le javascript qui est un outil pour utilisation de site dynamique.
Les notes = TP noté en fin de module et derniere demi journée 5 et 6 fevrier 2025

## Les API REST

Nous allons dans un premier temps utiliser les API avec le TP Stapi cinema

API : application programming interface : API proteger la base de donnée, de fournir les données dans un format souhaité, possibilite de customiser. Permet egalement de communiquer 2 logiciel en meme temps, faire communiquer des gens qui n'ont pas forcement connaissance de l'existence de l'autre.
C'est une interface de programmation qui permet de gerer de la base de donnée de maniere **securisée**; la gestion des rôles, gestions des droits.

-> permet à 2 application de communiquer sans se soucier de la maniere dont l'autre est codée.
Techno possible 
-REST (HTTP => Texte ou JSON)
-SOAP (XML) : a definir
-GraphQL (auto-doc en MBA 1) : gros points fort auto documentation, c'est de l'auto completion pas besoin de connaitre la techno pour utiliser
-RPC (données binaire type protobuf) : google, utilistaion tres petit, tres formaté echange de donnée binaire
-...

API REST : Une API REST est une interface de programmation d'application (API) qui permet d'établir une communication entre plusieurs logiciels. Grâce à elle, des logiciels d'applications utilisant différents systèmes d'exploitation peuvent interagir et partager des informations par l'intermédiaire du protocole HTTP.Une maniere uniforme mais non obligatoire de faire des API

REST: REpresentational State Transfer

Une maniere uniforme mais non obligatoire de faire des API
Sans connaitre API et de maniere uniforme de creer l'api
RestFul = API REST respectant les prinsipes de REST
- Stateless
- Uniform Interface
- Cacheable
- Clent-Server
- Layered System
- Code on demand (optionnel)

API RESTFUL - < CRUD>

- GET : /api/:pluralApiId                   get a list of entries
- POST : /api/:pluralApiId                  create an entry
- GET : /api/:pluralApiId/:documentId       get an entry
- PUT : /api/:pluralApiId/:documentId       update an entry
- DELETE : /api/:pluralApiId/:documentId    delete an entry


pluralApiId = restaurant**s**

Les méthodes PUT et PATCH ont des significations différentes :

- PUT, remplace les données par celle qui sont envoyées dans la requête.
- PATCH, permet la modification partielle d'une ressource en fusionnant les données envoyées avec les données déjà présentes ou grâce à l'utilisation d'opération de modification.
```nodeJS
const express = require('express)

```


DESCRIPTION DE L'API


Revoir les differents reponse HTML : http://mathartung.xyz/nsi/cours_requetehtml.html



Comment tester une API ?

- postman : interface first preference visuelle, partager le travail possible mais cela reste au format de postman, donc si changement probleme
- insomnia : interface first preference visuellepartager le travail possible mais cela reste au format de insomnia, donc si changement probleme
- curl : ligne de commande brut, c'est un outil de base il peut faire les requete http
- Rest Client VScode : on peut ecrire les requete la ou on a le code dans VS marche que dans les fichier HTTP.  genere des fichier un peur comme md dans le dossier de notre tavail
- Bruno : nouveau c'est un juste milieu entre postman et insomia et RestClient 
- fectch avec navigateur: possibilite mais seulement faire des get


Les Headless CMS

CMS = Content Management System

+Headless = sans interface graphique
= API sans coder

C'est Wordpress sans le front/Theme --> On va utiliser **Strapi**

Head c'est l'interface 
