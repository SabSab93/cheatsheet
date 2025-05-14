# Cours Docker

---

## 📋 Rendu

- TP final retraçant l’ensemble du cours  
- Évaluation écrite  
- Mise en place de Docker dans un projet existant

---

## 🚀 Introduction

Docker est une plateforme open-source qui permet de containeriser une application et son environnement pour :

- Uniformiser les environnements de développement, test et production  
- Isoler les dépendances et processus  
- Portabiliser les applications sur toute machine supportant Docker  

Un conteneur est une instance en cours d’exécution d’une image Docker, lui-même proche d’une machine virtuelle légère.

---

## ✨ Avantages de Docker

## ✨ Avantages de Docker (explications détaillées)

- **Flexible**  
  Toute application peut être transformée en conteneur.
  Docker peut contenir n’importe quelle application, qu’il s’agisse d’un simple script Python, d’un micro-service Node.js ou d’une base de données PostgreSQL. Vous choisissez l’image de base (Alpine, Debian, Python, etc.), puis vous ajoutez exactement ce dont votre app a besoin. Résultat : un environnement construit sur mesure, couche après couche, qui répond à vos besoins sans composants superflus.

- **Léger**  
  Contrairement aux machines virtuelles complètes, les conteneurs partagent le noyau du système hôte. Ils démarrent en quelques millisecondes et consomment seulement les bibliothèques et dépendances dont vous avez besoin. Une image Alpine Node.js peut peser moins de 50 Mo, là où une VM traditionnelle pèse plusieurs Go.

- **Portable**  
  Une image Docker fonctionne de la même manière sur votre poste de développement Windows/Mac, sur le serveur de test Linux en entreprise ou sur un cloud (AWS, GCP, Azure, Render…). Le conteneur embarque tout : système d’exploitation allégé, runtimes, bibliothèques et code applicatif. Vous n’avez plus de “ça marche chez moi, pas en prod”.

- **Auto-suffisant**  
  Chaque conteneur possède son propre espace isolé : fichiers, variables d’environnement, utilisateurs. Installer ou supprimer un conteneur n’affecte jamais les autres, ni l’hôte. Vous pouvez lancer deux versions différentes de la même app (v1.0 et v2.0) sans conflit de dépendances.

- **Scalable**  
  Vous pouvez cloner à l’identique un conteneur des dizaines ou centaines de fois en quelques secondes. En production, un orchestrateur (Kubernetes, Docker Swarm) surveille la santé des conteneurs et démarre automatiquement de nouvelles instances pour absorber la charge.

- **Sécurisé**  
  Les conteneurs utilisent les namespaces Linux et les cgroups pour isoler processus, réseau et système de fichiers. Même si un service est compromis, il reste confiné dans son conteneur. En plus, vous pouvez scanner vos images à la recherche de vulnérabilités avant chaque déploiement.

- **Auto-documenté**  
  Tout est consigné dans le **Dockerfile** : de la version de l’image de base au build des dépendances et à la commande de lancement. En quelques lignes de texte, un développeur comprendra comment assembler et exécuter votre application, et pourra reconstruire l’image de façon identique pour déboguer ou tester des correctifs.


---

## ⚙️ Docker vs Machine Virtuelle

| Caractéristique | Machine Virtuelle     | Conteneur Docker        |
|-----------------|-----------------------|-------------------------|
| Hyperviseur     | Oui                   | Non                     |
| Noyau dédié     | Oui                   | Non (partage le noyau)  |
| Démarrage       | Lent                  | Rapide                  |
| Poids           | Plusieurs GB          | Quelques MB à centaines |
| Isolation       | Fort                  | Sécurisé, mais plus fin |

---

## 📝 Structure d’un Dockerfile

Chaque instruction crée une **couche** (sauf WORKDIR, CMD, ENTRYPOINT, ENV…)  

```dockerfile
# 1. Base image
FROM alpine:3.18

# 2. Répertoire de travail
WORKDIR /app

# 3. Copier les fichiers de l’hôte
COPY package.json package-lock.json ./
COPY src/ ./src/

# 4. Installer les dépendances
RUN apk add --no-cache nodejs npm     && npm install

# 5. Documentation du port exposé
EXPOSE 3000

# 6. Commande au démarrage
CMD ["npm", "start"]
```

- **FROM** : image de base (Alpine, Debian, Python, Node, …)  
- **WORKDIR** : répertoire de travail pour les instructions suivantes, là où tout se passe
- **COPY** / **ADD** : copie des fichiers/sources dans l’image  
- **RUN** : exécute une commande au build (installation, compilation…)  
- **EXPOSE** : indique le port écouté (documentation)  
- **CMD** / **ENTRYPOINT** : commande par défaut au démarrage du conteneur

---

## ❌ .dockerignore

Pour exclure des fichiers du contexte de build (logs, `node_modules/`, secrets…)  

```gitignore
node_modules
dist
.vscode
README.md
.gitignore
.dockerignore
```

---

## Déploiement Docker : Méthodes manuelle et automatisée

---

### 1. Méthode manuelle

#### a. Structure du projet

À la racine de votre repo (même dossier que votre `Dockerfile`, `src/`, etc.) :

```bash
/mon-projet
├─ Dockerfile
├─ src/
├─ .dockerignore
└─ README.md
```

#### b. Commandes à lancer en local

Ouvrez un terminal dans la racine de votre projet et exécutez :

1. **Build**

    ```bash
    docker build -t <votre-user>/mon-app:tag-name .
    ```

2. **Push** (après login Docker)

    ```bash
    docker login -u <votre-user>                  # De GITHUB inscrire ensuite le token (bonne pratique) ou password de GitHub
    docker push <votre-user>/mon-app:tag-name
    ```

3. **Run**

    ```bash
    docker run -d --name mon-app -p 1992:3000 <votre-user>/mon-app:latest
    ```

4. **Inspect / Stop**

    ```bash
    docker ps
    docker stop mon-app/conteneurID
    docker rm mon-app/conteneurID
    ```

---

### 2. Méthode automatisée (CI/CD + Render)

#### a. Sur GitHub

1. **Créer** (ou modifier) le fichier :

    ```bash
    .github/workflows/docker-render.yml
    ```



2. **Y coller** ce workflow (adapté à vos secrets) :

```yaml
name: Docker
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Login to DockerHub
        run: echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login -u "${{ secrets.DOCKERHUB_USERNAME }}" --password-stdin
      - name: Build Docker image
        run: docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/demo-test:github-actions .
      - name: Push Docker image
        run: docker push ${{ secrets.DOCKERHUB_USERNAME }}/demo-test:github-actions
      - name: Render Build Hook
        run: |
          echo "Pinging Render build hook…"
          curl -X POST "${{ secrets.RENDER_BUILD_HOOK_URL }}"
```

3. **Ajouter** dans **Settings → Secrets and variables → Actions** :

    - `DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`  
    - `RENDER_BUILD_HOOK_URL` (votre HTTP Build Hook depuis le dashboard Render)

> Dès que vous pusherez sur `main`, GitHub Actions :  
> - buildera et pushera votre image Docker  
> - appellera le webhook de Render pour déployer automatiquement

#### b. Sur Render AVANT DE PUSH

1. Creer un new WebService et copier l'image 
1. Dans votre service Web (dashboard Render) → **Settings → Triggers**  
2. **Créer** (ou copier) l’**HTTP Build Hook**  
3. **Coller** l’URL comme secret `RENDER_BUILD_HOOK_URL` sur GitHub 

---

### 📝 En résumé

- **Manuellement** : vous exécutez les `docker build`, `docker push`, `docker run` dans votre terminal, dossier projet racine.  
- **Automatiquement** : vous versionnez un fichier YAML sous `.github/workflows/`, vous stockez vos secrets, et GitHub Actions + Render se chargent du reste.


## 🔄 CI & CD : définitions et intérêt

- **CI (Intégration Continue)**  
  Automatisation de la compilation et des tests à chaque modification de code, pour détecter rapidement les erreurs.
  1. **Build** de l’image Docker  
  2. **Tests** (lint, unit tests, etc.)  
  3. **Push** sur un registry

- **CD (Déploiement Continu)** 
  Automatisation du déploiement de l’application dès qu’un build et ses tests sont validés, pour livrer rapidement les nouvelles versions.
  1. **Trigger** d’un webhook (Render Build Hook)  
  2. **Déploiement** instantané de la nouvelle image sur l’infrastructure Render  

---

## 🎯 Pourquoi Docker + Git + Render pour CI/CD ?

1. **Reproductibilité**  
   - Docker encapsule l’environnement exact (OS, dépendances, variables), évitant le “ça marche chez moi”.  
2. **Automatisation**  
   - GitHub Actions orchestre le pipeline à chaque push : plus besoin de commandes manuelles.  
3. **Rapidité & Scalabilité**  
   - Les images légères démarrent en millisecondes, et Render gère automatiquement le scaling horizontal.  
4. **Fiabilité**  
   - Chaque build est tracé (logs, versions d’images, tags immuables), facilitant le rollback en cas de régression.  
5. **Séparation des responsabilités**  
   - Les développeurs se concentrent sur le code, CI/CD s’occupe du build & déploiement, et Render gère l’infrastructure.  
---

## 📦 Image vs Conteneur

- **Image** : modèle immuable composé de couches, stocké dans un registre, utilisé pour créer des conteneurs.  
- **Conteneur** : instance active d’une image, avec une couche d’écriture, des processus et un état isolés.  

---

## 🐳 Docker Compose

### Le rôle de Docker compose

docker compose permet de décrire l'architecture en microservices
de manière simple et efficace

Le fichier docker-compose.yml permet de décrire l'architecture
et de lancer les conteneurs en une seule commande

Plusieurs outils permettent de gérer un conteneur et ses interactions avec d'autres conteneurs

---

### Outils de docker compose

- **image** qui permet de spécifier l'image source pour le conteneur
- **build** qui permet de spécifier le Dockerfile source pour créer l'image du conteneur
- **volume** qui permet de spécifier les points de montage entre le système hôte et les conteneurs
- **restart** qui permet de définir le comportement du conteneur en cas d'arrêt du processus
- **secret** qui permet de définir les secrets utilisés par le conteneur
- **environment** qui permet de définir les variables d’environnement
- **depends_on** qui permet de dire que le conteneur dépend d'un autre conteneur
- **ports** qui permet de définir les ports disponibles entre la machine host et le conteneur
- **networks** qui permet de définir les réseaux disponibles entre les conteneurs

### Exemple de `docker-compose.yml`

```yaml
version: '3.7'

database:
  image: mysql:5.7
  restart: always
  environment:
    MYSQL_ROOT_PASSWORD: root
    MYSQL_DATABASE: database
    MYSQL_USER: user
    MYSQL_PASSWORD: password
  ports:
    - 3306:3306
  volumes:
    - ./database:/var/lib/mysql

wordpress:
  image: wordpress:latest
  restart: always
  depends_on:
    - database
  ports:
    - 80:80
  environment:
    WORDPRESS_DB_HOST: database:3306
    WORDPRESS_DB_USER: user
    WORDPRESS_DB_PASSWORD: password
    WORDPRESS_DB_NAME: database
  volumes:
    - ./wordpress:/var/www/html
```

### Commandes clés

```bash
docker-compose up -d             # Démarrer la stack en arrière-plan
docker-compose ps                # Voir le statut des services
docker-compose logs -f --tail=5  # Suivre les 5 dernières lignes de logs
docker-compose stop              # Arrêter la stack
docker-compose down              # Supprimer tous les conteneurs & réseaux
docker-compose config            # Valider la syntaxe du fichier
```

---

## 🏗️ Architecture Micro-services

- Plusieurs services indépendants, chacun dans son conteneur  
- Communication via réseaux Docker ou API REST  
- Bénéfices : équipes/autonomie séparées, montée en charge ciblée, hétérogénéité technologique

---

