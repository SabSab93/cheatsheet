# Mobile hybride

## Jour 1

PWA : progresive webapp abjectif d'avoir un site adapter au mobile
React + PWA alors qu'on maitrise totalement Angular. En mobile moins de debat pour le mobile IOS c'est un mac c'est le seul OS qui permet de developer du mobile. Pour le dev en genrale on peut utiliser windox, linux... pas de preference. 
De meme pour les framework JS, pareil chacun à ses avantages et inconvenients. React est le framework le plus utiliser dans le monde du dev mmobile hybride. Historiquement grosse dif entre je fais du mobile avec react native (couche abstraction perf ok); ou le choix react native script c'est un peu comme du electron qui permet de lancer l'application (voir les def). Modulo Lynx peut etre un concurent de react natif potentiel.



### React est un framework JS

Ca ne change pas trop Components avec des focntion, des props qui est un parametre des fonctions, des etats qui sont des variable locales des fonctions. 
Events evenement des fonctions avec un callback une fonction qui se lance
Données calculees qui est variables calculées des fonctions 


CF cours rapide sur React

Mauvais patern sur React d'utiliser useRef a eviter !!!!!

### Live coding

On va realiser les compteurs :
- Creer un compteur avec react
- Creer un composant compteur et utilsier une app 
- Ajouter un bouton pour incrementer le compteur
- Au montage du composant

### 3 methode dev mobile

3 possibilite de faire du dev mobile qui doit etre quel est le meilleur choix pour le projet : 
- App Web, un peu boostée (PWA), mais pas trop (Ionic) : PWA est une map web qui est booster exemple X Un service worker c'est une tache de fond qui permet de gerer le cache ce qui permet que les PWA sont prete pour offline
- App Hybride (React Natiive, Flutter, peut etre Lynx) on fait 1 code base pour 2 appli differente : deplacer les elements etc, 3d,..
- App Native (Switch, Kotlin, Java, Objective-C) on doit faire 2 code bas pour 2 aplli differente : jeu ou connecter iot


Faire du referencement dans un store on crrer une application vitrine qui ramene vers le store dans celui ci on doit mettre des mots cles, mettre en avant les telechargeemnt et commentaire
et c'est pour ca que le PWA est bien car ca ne coute rien
Mais possibilite de passer par PWA pour faire l'app mobile, et possibilite de passer PWA à app Hybride c'est le dev full stack ++


Electron c'est un chromium  VsCode c'est un chromium 
Tauri : https://v2.tauri.app/

https://nativescript.org/

c'est mieux  : https://lynxjs.org/


L'ordre à son importance
- TJM
- Temps de developpement
- Reutilisation du code
- Performance 
- Experience utilisateur
- Maintenance 


Une web app ne devrait pas etre autre choses qu'une PWA

- C'est trivial donc on le fait
- C'est trop bien sur le papier donc on evangelise
- En vrai c'est pas si ouf souvent problematique avec Apple


Worker c'est lancé un autre programe js qui fonctionne en fond et renvoie le resultat une fois finit ca permet de paralelliser le code
Service worker est un worker dedié au web
Le service worker va gerer les push notif une fois qu'il recoit un event push notif il renvoit à l'app
Il sert aussi au background task app n'est pas lancé qu'elle fasse des choses
tache de fond qui fait des choses pendant que l'app est fermé exemple les app podometre

Il existe plusieurs  methode de cache :

- cache only : pas interessant
- network only : exemple la connaissance meteo , ou connaissance de la bourse : connaissance de la derniere donnée a jour on s'en fiche de l'ancienne donné 
- cache first : si il y a du cache il repond à la page si pas de cache il recupere le cache du network exemple asset 
- networkfirt je veux des données toujours a jour par contre si j'ai pas de network, on recupere la derniere requete exemple la prise de rendez vous
- stale while revalidate 


https://vite-pwa-org.netlify.app/


Workbox 2 gros module
- generateSW : https://vite-pwa-org.netlify.app/workbox/generate-sw.html on vient configuerer avec ça plutot que le deuxeimen et il voudra recuperer le type de cache qu'on utilisera : https://developer.chrome.com/docs/workbox?hl=fr

- injectManifest



### Formulaire de saisie d'adresse 
creer une PWA
creer un formulaire de saisie d'adress
utiliser l'API du gouvernement pour la recherche d'adresse
Utiliser trottle vs debounce :
![alt text](image-5.png)


### Correction du TP formulaire


## Jour 2 et 3 ou bien jour 3 et 4 devoir à faire sur le mobile


