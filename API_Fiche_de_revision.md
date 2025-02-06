# Feuille de révision : API avec Node.js et Express

## Définition d'une API

- **API (Application Programming Interface)** : Interface permettant à deux applications de communiquer entre elles.
- Une API peut être **publique, privée ou payante** (ex. Google Maps pour Uber).
- Types d'API : REST, SOAP, GraphQL, RPC.
- **REST API** (REpresentational State Transfer) :
  - Basée sur HTTP (GET, POST, PUT, DELETE, PATCH).
  - Stateless, Uniform Interface, Cacheable, Client-Server, Layered System, Code on Demand (optionnel).
  - Respecter REST permet une meilleure intégration web.

## Définitions des termes principaux

- **Stateless** : L'API ne conserve pas l'état des requêtes précédentes.
- **CRUD** : Acronyme de Create, Read, Update, Delete, représentant les opérations de base d'une API.
- **Middleware** : Fonction exécutée avant que la requête n'atteigne la route finale.
- **CORS (Cross-Origin Resource Sharing)** : Mécanisme permettant à une API d'être accessible depuis différents domaines.
- **ORM (Object-Relational Mapping)** : Outil permettant d'interagir avec une base de données via des objets.
- **JWT (JSON Web Token)** : Format de token utilisé pour l'authentification sécurisée.
- **Bearer Token** : Token d'accès envoyé dans l'en-tête d'une requête HTTP pour authentifier l'utilisateur.
- **Hashing** : Technique de cryptographie permettant de stocker les mots de passe de manière sécurisée.
- **Prisma** : ORM moderne permettant d'interagir facilement avec une base de données.
- **Express.js** : Framework Node.js facilitant la création d'API et la gestion des routes.
- **Postman** : Outil utilisé pour tester les API.
- **OAuth** : Protocole permettant l'authentification et l'autorisation via un service tiers (Google, GitHub, etc.).
- **.env** : Fichier permettant de stocker des variables d'environnement de manière sécurisée.

## Générer une clé secrète ou un hash secret

- **Génération d'une clé secrète** en ligne de commande :
  ```sh
  node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
  ```
- **Génération d'un hash secret avec bcrypt** :
  ```sh
  node -e "require('bcrypt').hash('monSecret', 10, (err, hash) => console.log(hash))"
  ```

## Initialiser un projet Node.js avec Express et Prisma

1. **Initialisation du projet**

```sh
mkdir mon-projet-api
cd mon-projet-api
npm init -y
```

2. **Installation des dépendances**

```sh
npm install express dotenv cors jsonwebtoken bcrypt
npm install prisma --save-dev
```

3. **Initialisation de Prisma**

```sh
npx prisma init
```

4. **Création du fichier principal**

```sh
touch index.js
```

5. **Lancer le serveur**

```sh
node index.js
```

## Les méthodes HTTP principales

- **GET** : Récupérer des données.
- **POST** : Créer une nouvelle ressource.
- **PUT** : Mettre à jour une ressource en remplaçant toutes ses données.
- **PATCH** : Mettre à jour partiellement une ressource.
- **DELETE** : Supprimer une ressource.

## Tester une API

- **Outils** : Postman, Insomnia, cURL, Rest Client (VS Code), Bruno, fetch avec navigateur.
- Vérifier les **codes de réponse HTTP** (200, 201, 400, 401, 403, 404, 500, etc.).

## Headless CMS & Strapi

- **CMS** : Content Management System (ex. WordPress).
- **Headless CMS** : Expose les données sous forme d'API, sans interface graphique.
- **Strapi** : CMS headless open-source qui permet de créer une API facilement.

## ORM (Object-Relational Mapping)

- Permet d'interagir avec une base de données relationnelle en manipulant des objets.
- **Exemples** : Sequelize, Prisma (utilisé dans le TP), TypeORM.
- **Intérêt** : Ne pas écrire de SQL directement, synchronisation des données et gestion des migrations.

## Sécurité et authentification

- **Authentification** : Vérification de l'identité (ex. login/mot de passe, 2FA, OAuth, passkeys).
- **Autorisation** : Vérification des droits d'accès (ex. admin vs utilisateur lambda).
- **JWT (JSON Web Token)** :
  - Contient trois parties : Header, Payload, Signature.
  - Généré par le serveur et stocké par le client.
  - Permet une authentification sans stocker l'état côté serveur.
  ```js
  const jwt = require("jsonwebtoken");
  const token = jwt.sign({ userId: 123 }, "secret-key", { expiresIn: "1h" });
  jwt.verify(token, "secret-key");
  ```
- **Bcrypt** : Pour hasher les mots de passe.
  ```js
  const bcrypt = require("bcrypt");
  const hashedPassword = await bcrypt.hash("monMotDePasse", 10);
  const match = await bcrypt.compare("monMotDePasse", hashedPassword);
  ```

## API et Sécurité

- **CORS** : Activer les accès cross-origin.
  ```js
  const cors = require("cors");
  app.use(cors());
  ```
- **.env pour gérer les variables sensibles**
  ```sh
  npm install dotenv
  ```
  ```js
  require("dotenv").config();
  console.log(process.env.SECRET_KEY);
  ```

## Générer un token JWT

```
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

## Déploiement

- **Base de données en ligne** : Neon (PostgreSQL en cloud).
- **Hébergement** : Vercel (serveurless pour Next.js) ou Railway/Render.

## À retenir

- **REST API** : Basée sur HTTP, CRUD, stateless.
- **Express.js** : Framework Node.js pour API.
- **Sécurité** : JWT, Bcrypt, OAuth.
- **ORM** : Prisma pour gérer la base de données.
- **Testing** : Postman, Insomnia, cURL.