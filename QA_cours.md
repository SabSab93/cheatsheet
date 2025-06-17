# Cours : Les fondamentaux du **testing** en développement logiciel

---

## Chapitre 0 – Contexte : Qualité logicielle et rôle des tests

1. **Qualité logicielle**  
   La qualité du code consiste à s’assurer qu’il :  
   - Fait ce qu’il doit faire  
   - Suit un style cohérent  
   - Est facile à comprendre  
   - Est bien documenté  
   - Peut être testé  

2. **Pourquoi tester ?**  
   - **Détecter tôt** les régressions et bugs  
   - **Garantir** la stabilité du code au fil des évolutions  
   - **Assurer** la confiance des utilisateurs et des équipes  
   - **Chiffrer** la couverture et la qualité du code  

---

## Chapitre 1 – Définitions et types de tests

### 1.1 Qu’est-ce qu’un test ?  
> Un test, c’est confronter une **assertion** à une **réalité** pour valider un comportement attendu.  

### 1.2 Les niveaux de tests  

| Niveau              | Qui écrit ?       | Front / Back                           | Portée                                    | Description                                                         | Exemple d’outil                   |
| ------------------- | ----------------- | -------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------- | --------------------------------- |
| **Tests unitaires** | Développeurs      | Front **et** Back                      | Une **unité** (fonction, méthode…)       | Exerce un bout de code isolé, sans accès à la BD ni aux API externes (mocks/stubs) | Jest, Mocha                       |
| **Tests d’intégration** | Équipe QA / DevOps | Plutôt **Back** (mais possible en Front) | Plusieurs modules ensemble                | Vérifie que plusieurs composants (service, base de données…) communiquent correctement        | Postman, Supertest                |
| **Tests E2E**       | QA / PO / Dev     | **Front → Back**                       | Scénarios utilisateur complets            | Simule un utilisateur final (navigateur + serveur + base)                        | Playwright, Cypress, Puppeteer    |

Unitaires : vous écrivez le test avant ou après la fonction, pour valider un petit morceau de code ; ils concernent autant le code front (composants React, helpers JS) que back (fonctions Node.js, classes Java).

Intégration : vous testez la bonne communication entre plusieurs briques côté serveur (API ↔ BD) ou, en front, entre un store Redux et des composants.

E2E : vous pilotez le vrai navigateur (Playwright/Cypress) pour valider un scénario « de l’UI jusqu’à la base » – c’est ce que verrait un utilisateur final.

> **Astuce** : on vise un **petit nombre** de tests E2E (coûteux), un volume **moyen** de tests d’intégration et un **grand nombre** de tests unitaires (rapides à maintenir).

---

## Chapitre 2 – Tests unitaires

### 2.1 Pourquoi et comment ?  
- **Isolation totale** : on n’appelle jamais de base de données ni d’API externe – on utilise mocks et stubs  
- **Unité** : chaque test porte sur une seule unité de code  
- **Rapidité** : exécution en quelques millisecondes à secondes  
- **Automatisation** : résultat Pass/Fail géré par un test runner  
- **Rejouabilité** : même résultat quel que soit l’environnement  

### 2.2 Les critères d’un **bon** test unitaire  
1. **Unité**  
2. **Isolation** (Mocks/Stubs)  
3. **Rapidité**  
4. **Indépendance** (ordre des tests non impactant)  
5. **Automatisation** (scriptable)  
6. **Rejouabilité** (idempotence)  

---

## Chapitre 3 – Tests d’intégration

### 3.1 Objectif  
Vérifier que plusieurs composants ou services fonctionnent correctement lorsqu’ils sont assemblés.

### 3.2 Caractéristiques  
- **Portée** : base de données de test, services internes (pas d’appels externes)  
- **Isolation partielle** : on peut utiliser des bases de données en mémoire ou conteneurs Docker  
- **Durée** : de quelques centaines de millisecondes à quelques secondes  
- **Automatisation** : inclus dans la CI pour détecter les problèmes d’assemblage  

### 3.3 Bonnes pratiques  
- Préparer une **fixture** ou base de données dédiée  
- Réinitialiser l’état entre chaque test  
- Couvrir les **flux critiques** (CRUD, authentification, appels inter-services)  
- Utiliser des outils comme Postman/Newman, Supertest, TestContainers  

---

## Chapitre 4 – Approches TDD, BDD & co.

| Approche | Objectif principal | Spécificité                                                       |
| -------- | ------------------ | ----------------------------------------------------------------- |
| **TDD**  | *Drive design*     | On écrit d’abord le test unitaire, puis le code pour le passer    |
| **ATDD** | *Alignement métier*| Tests d’acceptation définis avant le code, impliquant PO & QA     |
| **BDD**  | *Spécification*    | Tests rédigés en langage proche du domaine (`GIVEN/WHEN/THEN`)    |

---

## Chapitre 5 – Écosystème de tests JavaScript

- **Jest**  
  - Runner & assertion library  
  - Syntaxe `expect(...).toBe(...)`, `it()`, `describe()`  
  - Couverture de code intégrée  
- **Cucumber** (BDD)  
  - Scénarios `.feature` en langage naturel  
- **Playwright** / **Puppeteer** (E2E)  
  - Contrôle du navigateur en Node.js  
  - Multi-navigateur (Chromium, WebKit, Firefox)  
- **Cypress** (E2E)  
  - Temps réel, dashboard interactif  

---

## Chapitre 6 – Intégration tests & CI/CD

1. **Ajouter les tests** dans le pipeline de CI (GitLab CI, GitHub Actions…)  
2. **Échecs bloquants** pour commits/merges  
3. **Rapports** de couverture et de logs  
4. **Déploiement continu** : si les tests passent, on déploie automatiquement  

---

## Chapitre 7 – Tests end-to-end (E2E)

- **But** : valider un **scénario utilisateur** complet  
- **Limites** :  
  - Longs à exécuter  
  - Fragiles (changement DOM)  
- **Bonnes pratiques** :  
  - Utiliser des attributs test-id  
  - Isoler l’environnement (serveur X, bases de données de test)  
  - Maintenir une documentation claire des scénarios  



## Partie II – Ressources utiles

| Outil / Lien                                              | Description rapide                                                                           |
| --------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **ESLint**<br>https://eslint.org/                         | Linter JavaScript : détecte erreurs de style et de syntaxe, applique des règles configurables. |
| **Prettier**<br>https://prettier.io/                      | Formateur de code : uniformise le style (indentation, quotes, points-virgules).             |
| **Bit**<br>https://bit.dev/                               | Catalogue de composants isolés, partage et versioning de modules UI.                        |
| **Storybook**<br>https://storybook.js.org/tutorials/intro-to-storybook/react/en/get-started/ | Développement et documentation de composants UI en isolation.                                |
| **React UI Storybook**<br>https://react-ui-storybook.vercel.app/ | Exemples et docs de composants pré-développés.                                              |
| **Docusaurus**<br>https://docusaurus.io/docs/markdown-features | Générateur de sites de documentation à partir de Markdown.                                  |
| **Husky**<br>https://typicode.github.io/husky/            | Hooks Git en local : linter/tests avant commit pour garantir la qualité.                    |
| **Blog DevOps**<br>https://blog.stephane-robert.info/docs/devops/racines/ | Introduction aux bases du CI/CD et aux pipelines DevOps.                                    |
| **Cucumber.js**<br>https://cucumber.io/docs/installation/javascript/ | Framework BDD JavaScript pour scénarios en langage naturel.                                 |
| **Jest Cheat Sheet**<br>https://github.com/sapegin/jest-cheat-sheet | Raccourcis et tips pour Jest (matchers, configuration, mock).                               |
| **Playwright**<br>https://playwright.dev/                 | Automatisation de navigateurs pour tests E2E : multi-langages, multi-navigateur.            |
| **Playwright Locators**<br>https://playwright.dev/docs/locators#locate-by-test-id | Guide sur les stratégies de sélection d’éléments (`data-test-id`, rôle ARIA…).             |

---

## Annexes : **Cheat-sheets**

### A. Template **AAA** pour tests unitaires  
```txt
Arrange  : Initialisation des objets et données de test
Act      : Appel de la fonction / unité testée
Assert   : Vérification des résultats attendus
