<h1 align="center">Conception Logicielle</h1>

Metier proche du PO (product owner)
beaucoup de methodo dans la conception de logicielle c'est la phase avant de coder


UML : language

## Modélisation

Modéliser : abstraction d'un phenomene complexe pour se rapprocher au mieux de la réalité. Il n'y a pas de point de vue parfait. Jugement, experience,...
Se rapprocher d'une reélité avec son propre point de vue; notion subjective.

Cette notion est tres forte dans le métier du PO qui est l'intermediare netre le dev et client

Informatisation ! hardware + software: ce sont des outils qu'on utilisera pour creer le process 

SI: Systeme d'information = Data : la matire s'appelle SI; en entreprise il y a un pole SI (grande E) à ne pas confondre avec DSI (admin, reparation ordi...)
Cela se rapproche à des poste de type ingé bac+5

Modélisation : 2 grands concepts 
je pars d'un cachier des charge pour arrivée à 
- de la POO (programmation orienté objet) 
- schema de base de donnée


## Introduction

Les devs sont mauvais dans l'ensemble en 1995 constat selon les chiffres de la ***diapo***
- 9 % seulement des projet etaient conformes aux prévision initales
- 50% avaient subi des depassement en cout et delai d'un facteur 2 à 3 avec diminution du nombre des fonction offerte
- 30 int ete purement abandonnée


## Génie Logiciel

objectif : optimiser les coûts du developpement logiciel pour contrer :(charge / delai 2 notions differentes = diagramme de Gant)
-   augmentation des coûts 
-   difficultés de maintenance et d"volution
-   non-fiabilité
-   non-respect des spécifications
-   npn-respect des délais

-> Maintenance = 53 % du coût total du logiciel


## Pourquoi modéliser

Language commun qui permet de communiquer entre technicien et ceux qui sont la pour un besoin. Explorer et documenter un probleme avec des outils abstraits cad toujours etre à jour / non multi techniques, etat de l'art actuel du logiciel.
La conception permet d'eclairecie le dev et egalement le client qui est confrontrer à une analyse de sa demande: les points qui ne fonctionne pas etc...


## Cycle en V

La matiere a ete créée selon le cycle V

cela se confrontre à l'idée Agilité

Idée du cycle V:

specification:  Avant tout chose on reflechit, on passe beaucoup de temps à reflechir poser des questions, triturer etc... spec interview avec le clien, faire de la veille techno

conception detaillé: comment concretement doit se passer dans nos codes pour creer le logiciel.

codage: on fait des petit bout de code

integration : on rassemble nos bout de code

qualification : mettre des metrique, cad chiffrer sur nos codes, juger le code (possibilité de retour avec le codage si par exemple: le temps de chargeemnt est trop long)

test unitaire : on fait du recetage cad utiliser le logiciel

validation : QA quality assurance (un métier à regarder) test du logiciel et valider

resultat du cycle en V c'est qu'a la fin de toutes ses etapes on peute etr loin de la demande client , on est loin du client dans le bas du V 

partie haute : client 

partie bas : developpement

vs agilité qui l'objectif est d'etre toujours proche du client

cycle en V c'est parfait pour parle de syste d'info etc... il faut etre bon dans les specs et travailler à petit echcelle pour que le cycle V soit optimal


## Agilité/Lean

Agilité est une methode de travail, pas une methode de conception. On avance en etape sprint step by step pour avance jusqu'au resultat demandé; le logiciel est utilisable rapidement. Le client a la visibilité rapidement sur son livré.
Penibilité au travail : il faut produire vite et mal, pb de repasser dessus sans cesse. Potentiellement on bosse sur un truc qu'on va devoir jeter; On perd la noblesse de coder proprement. 

C'etait mieux avant VS il faut tout changer tout le temps !


## Programmation structurée vs POO

POO : architecture du systeme est dictée par la struture du probleme: exemple un humain avec une taille, un poids

Structurée = fonctions qui modifient de la date, l'architecture du systeme est dictée par la réponse au probleme


Le livrable qu"on arrive rapidement cest avec le POO
- l'identité
- les attributs
- les méthodes 

La difficulté de cette modélisation consiste à créer une representation abstraite, sous forme d'objets,d'entités ayant une existence matérielle (chien, voiture, ampoule, personne,...) ou bien virtuelle (client, temps,...).


Héritage : transmission de caracteristique d'un objet à un enfant (attributs + methodes)

Polymorphisme : 

A COMPLETER !!!


## Historique 

A COMPLETER !!!

Smalltalk 1er language, puis evolution C+++ langage C + POO apparu en 1982
et java apparait 20 ans apres


## UML

Unified Modelin Language est né d'un effort de convergence. Il existe maintenant d'autres langages de modélisation : 
- plantUML : https://plantuml.com/fr/ plus complet et plus recent que Mermaid : probleme fortement lié à java mais fonctionne avec la bonne extension
- BPM
- SysML
- Archimate

A regarder :  

C'est un peu comme les gitflow, il y a des variantes mais UML reste tres utilisé

Mermaid qu'on va utiliser, on va creer des graphiques a partir de code


## Mermaid comme alternative

Markdown + Mermaid = UML et tout ca avec du git hub 

https://www.mermaidchart.com/landing?utm_source=google_ads&utm_medium=primary_search&utm_campaign=mermaidecosystemfocus-G&gad_source=1&gclid=Cj0KCQjwveK4BhD4ARIsAKy6pMLQJO05CoDLMsOO7selpQw9g2Y0-MoT8Am_KXCGcszvFJ_IeELS85MaAkgtEALw_wcB


 dbdiagram https://dbdiagram.io/home


Differentes types de diagrammes pour la matiere :
-   use case
-   Sequence
-   Class

Pas de MCD : modele conceptiel de donnée

# TP tunnel d'achat

-   creation de projet
-   presentation au reste de la classe
-   participation à la confrontation de nos idées face aux autres

choisir une partie du tunnel d'achat et dle modeliser en UML selon vos idées / préfences.

Etre capable de le presenter à l'oral et de confronter vos idées avec celles des autres

Dans une approche en cycle en V, comment integrer ce tunnel d'achat dans un projet de site e-commerce ? on ne va pas jusqu'à l'étape de codage. 

on part du use case 

en passant par le diagramme de séquence

jusqu'au diagramme de classe et la POO

jusqu'au MCD

Undev n'est pas là pour coder. C'est un outil au service du métier. Il doit comprendre le métier et **améliorer les processus**. 

La technique est un moyen, pas une fin. Le role de PO


# Use case

Un "use case" (ou "cas d'utilisation" en français) est une description des interactions entre un utilisateur (ou un autre système) et un système logiciel pour atteindre un objectif spécifique. 

Les use cases sont souvent utilisés dans le cadre de l'ingénierie logicielle et de la conception de systèmes pour capturer les exigences fonctionnelles d'un système.

Les use cases sont souvent représentés graphiquement à l'aide de diagrammes de cas d'utilisation, qui montrent les acteurs et les use cases ainsi que leurs relations. Ils sont également décrits textuellement dans des documents de spécification des exigences.

exemple actor=coiffeur : ces scenarios sont coiffer / prise RDV /encaisser / nettoyer

On veut livrer un logiciel (prise de rendez-vous et encaisser) donc on devra retirer les scenario qui ne rentre pas dans le besoin.
reste : prise rdv / encaisser

on ressors un use case : lister dispo / prise RDV anonyme ou specifique /encaisser 

Acteurs : Représentent les entités externes qui interagissent avec le système. Peut etre plusieurs suivant les scenarios qu'ils ont, cela peut prioriser nos etapes


2eme etape diagramme de sequence

Un diagramme de séquence est un type de diagramme utilisé dans la modélisation des systèmes, notamment dans le cadre de l'UML (Unified Modeling Language). Il représente les interactions entre différents objets ou acteurs dans un système au fil du temps. Les diagrammes de séquence sont particulièrement utiles pour visualiser les flux de messages entre les objets et pour comprendre la chronologie des événements dans un scénario spécifique.

![diagramme de sequence](image/ConceptionLogiciellePart/diagramme_de_sequence.png)

https://laurent-audibert.developpez.com/Cours-UML/?page=diagrammes-interaction#L7-2

![diagramme de communication](image/ConceptionLogiciellePart/diagramme%20de%20communication.png)

![diagramme de sequence](image/ConceptionLogiciellePart/UML_-_Diagramme_de_séquence_-_Exemple.png)



un acteur peut s'auto appeler 


dans les classes il y a attribut et methode

```typescript
class Voiture {
    constructor(
        public couleur: string,
        public vendue: boolean = false
    ){}

    rouler (){
        console.log("je roule")
    }

    vendre(){
        this.vendue = true
    }
    getStatus(){
        return this.vendue ? "vendue" : "pas vendue"
    }
}

const voitureNoire = new Voiture ("noire", false)
const voitureNoireEstVendueAvant = voitureNoire.getStatus()
console.log("Avant vente La voiture noire est " + voitureNoireEstVendueAvant)

voitureNoire.vendre()
const voitureNoireEstVendue = voitureNoire.getStatus()

console.log("La voiture noire est " + voitureNoireEstVendue)


const voitureRouge = new Voiture ("rouge")
voitureRouge.rouler()
const voitureBleu = new Voiture ("bleu")

```
