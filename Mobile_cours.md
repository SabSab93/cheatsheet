# Développement Mobile Hybride & PWA — Cours Complet

B3 Dev Grenoble 2025 — Synthèse basée sur vos notes et les slides du professeur.

---

## Sommaire

1. [Panorama des approches mobiles](#1-panorama-des-approches-mobiles)
2. [Progressive Web Apps (PWA)](#2-progressive-web-apps-pwa)
3. [React pour le Web & le Mobile](#3-react-pour-le-web--le-mobile)
4. [React Native & Expo](#4-react-native--expo)
5. [Outils et frameworks alternatifs](#5-outils-et-frameworks-alternatifs)
6. [Concepts transverses](#6-concepts-transverses)
7. [Glossaire (termes techniques)](#7-glossaire-termes-techniques)
8. [Liens & Ressources commentées](#8-liens--ressources-commentées)
9. [Cheat‑sheets essentielles](#9-cheat‑sheets-essentielles)

---

## 1. Panorama des approches mobiles

Il existe plusieurs méthodes pour développer des applications mobiles, chacune ayant ses avantages et ses inconvénients selon le contexte et les besoins du projet.

* **Web App + PWA** — Applications web améliorées (HTML / CSS / JS). Déploiement ultra‑rapide, coût minimal, parfaite visibilité SEO, mais accès matériel limité et performances moindres.
* **Hybride** (React Native, Flutter, Lynx) — Une base de code unique pour iOS et Android, ponts natifs pour la caméra, le GPS, etc. Meilleures performances que les PWAs, mais encore un léger sur‑coût par rapport au natif.
* **Native** (Swift, Kotlin, Obj‑C, Java) — Code spécifique par plateforme, accès matériel complet et performances maximales. Idéal pour les jeux 3D, la réalité augmentée ou les apps fortement intégrées à l’OS, mais coûteux.

| Solution                                  | Base de code      | Accès matériel    | Perf.  | Quand l’utiliser ?                  |
| ----------------------------------------- | ----------------- | ----------------- | ------ | ----------------------------------- |
| **Web App + PWA**                         | 1 (Web)           | Limité (APIs Web) | ⚪️⚪️⚪️ | MVP, budget serré, visibilité Web   |
| **Hybride** (React Native, Flutter, Lynx) | 1                 | Ponts natifs      | ⚪️⚪️⚫️ | Produit cross‑platform, UI 2D riche |
| **Native** (Swift, Kotlin, Obj‑C, Java)   | 2 (iOS + Android) | Complet           | ⚫️⚫️⚫️ | Jeux, VR, accès profond à l’OS      |

> **Critères de choix** — TJM (coût), délai, réutilisation de code, performances, expérience utilisateur, maintenance.

---

## 2. Progressive Web Apps (PWA)

Une **PWA** est une application web qui se comporte comme une application native : installable, hors‑ligne, notifications push, écran d’accueil.

### 2.1 Ingrédients obligatoires

| Élément             | Rôle                                                    |
| ------------------- | ------------------------------------------------------- |
| **HTTPS**           | Sécurise et permet les Web APIs avancées                |
| **`manifest.json`** | Métadonnées (nom, icônes, thème, `display: standalone`) |
| **Service Worker**  | Script exécuté en arrière‑plan (cache, offline, push)   |

### 2.2 Stratégies de cache (Workbox)

| Stratégie                | Idéal pour                        | Comportement                  |
| ------------------------ | --------------------------------- | ----------------------------- |
| `cache‑only`             | Assets figés                      | Ne touche jamais le réseau    |
| `network‑only`           | Données critiques (météo, bourse) | Toujours le réseau            |
| `cache‑first`            | Logos, polices                    | Servez le cache, sinon réseau |
| `network‑first`          | Contenu éditorial                 | Essaye réseau, fallback cache |
| `stale‑while‑revalidate` | Mix perf/fraîcheur                | Sert le cache puis met à jour |

### 2.3 Workbox + Vite PWA (Quickstart)

```bash
npm install -D vite-plugin-pwa workbox-window
```

`vite.config.ts` :

```ts
import { VitePWA } from 'vite-plugin-pwa';
export default defineConfig({
  plugins: [
    VitePWA({
      registerType: 'autoUpdate',
      workbox: {
        runtimeCaching: [
          {
            urlPattern: /\.(?:png|jpg|jpeg|svg)$/,
            handler: 'CacheFirst'
          }
        ]
      }
    })
  ]
});
```

---

## 3. React pour le Web & le Mobile

React est une bibliothèque JS déclarative basée sur des **composants**.

### 3.1 Concepts clés

* **Composant** — Fonction retournant du JSX.
* **Props** — Paramètres passés du parent à l’enfant.
* **State** — État local via `useState`.
* **Effets** — `useEffect` pour effets de bord.

### 3.2 Exemple détaillé Props (Parent → Enfant)

```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <Child value={count} onIncrement={() => setCount(c => c + 1)} />
  );
}
function Child({ value, onIncrement }) {
  return <button onClick={onIncrement}>Compteur : {value}</button>;
}
```

### 3.3 Throttle vs Debounce

|          | **Throttle**                | **Debounce**               |
| -------- | --------------------------- | -------------------------- |
| Principe | Limite la fréquence d’appel | Attend la fin d’une rafale |
| Exemple  | Scroll infini               | Champ de recherche         |

> 🔴 **Anti‑pattern** : stocker un état dynamique dans `useRef` au lieu de `useState` ou `useReducer`.

---

## 4. React Native & Expo

React Native traduit des composants React en **vues natives**. Expo fournit un CLI prêt à l’emploi.
React Native

Ton code React (JSX + JavaScript) tourne dans un thread JS.

Ce thread envoie des messages au “bridge” (= pont) fourni par React Native.

Le pont demande alors au système d’exploitation (iOS ou Android) de créer de vrais boutons, listes, champs texte, etc. — les mêmes que quand tu codes en Swift ou Kotlin.

Résultat : pas de WebView, l’UX est fluide et les gestes/animations restent natifs ; toi, tu restes dans l’écosystème React (hooks, props, hot-reload).

Expo

Pense-le comme une boîte à outils + un simulateur.

- Une seule commande :npx create-expo-app ⇒ projet prêt, serveur de dev lancé, appli “Expo Go” sur ton téléphone pour tester en live (scan d’un QR-code).
- Fournit des modules unifiés pour l’appareil photo, les capteurs, les notifications, sans avoir à manipuler Xcode ni Android Studio.


En résumé : React Native = même logique React, mais rendu 100 % natif.
Expo = la couche qui simplifie l’installation, le test et la distribution.

### 4.1 Mise en route

```bash
npx create-expo-app@latest myApp
cd myApp
npm run start -- --tunnel
```

### 4.2 UI & APIs clés

| Élément                     | Rôle                           |
| --------------------------- | ------------------------------ |
| **SafeAreaView / Provider** | Gère encoches & Dynamic Island |
| **ScrollView / FlatList**   | Listes performantes            |
| **Platform**                | Brancher selon iOS / Android   |
| **StyleSheet**              | Styles Flexbox‑like            |

### 4.3 Gestion d’état globale

* **Context API** : évite le prop‑drilling.
* **Zustand** : micro‑store basé hooks.
* **MobX** : observables réactifs.
* **`useReducer`** : mini‑Redux natif React.

---

## 5. Outils & frameworks alternatifs

| Projet           | Catégorie   | Particularité                           |
| ---------------- | ----------- | --------------------------------------- |
| **Lynx**         | Hybride     | Promet perf native sans pont JS ↔ natif |
| **NativeScript** | Hybride     | XML UI, accès natif direct              |
| **Flutter**      | SDK Google  | Dart + rendu Skia                       |
| **Electron**     | Desktop Web | Chromium + Node                         |
| **Tauri**        | Desktop Web | WebView + backend Rust, binaire léger   |

---

## 6. Concepts transverses

* **Worker & Service Worker** — Threads JS en arrière‑plan.
* **WebAssembly (WASM)** — Exécuter C/Rust/Go quasi natif.
* **TensorFlow\.js** — ML client ou React Native.
* **API Adresse Gouv** — Autocomplétion française.
* **Expo BarCodeScanner** — QR/EAN caméra.

---

## 7. Glossaire

| Terme                   | Définition                                       |
| ----------------------- | ------------------------------------------------ |
| **PWA**                 | Web app installable, offline.                    |
| **Service Worker**      | Script hors‑page interceptant réseau + push.     |
| **Manifest**            | Fichier JSON décrivant PWA.                      |
| **Workbox**             | Lib Google pour générer SW.                      |
| **Context API**         | Partage de valeur sans prop‑drilling.            |
| **Throttle / Debounce** | Limitation / différé d’exécution d’une fonction. |
| **SafeArea**            | Zone écran sans encoche.                         |
| **WASM**                | Format binaire web haute perf.                   |
| **TJM**                 | Taux Journalier Moyen freelance.                 |

---

## 8. Liens & Ressources

| URL                                                                                                                        | Pourquoi c’est utile ?              |
| -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| [https://vite-pwa-org.netlify.app/](https://vite-pwa-org.netlify.app/)                                                     | Docs vite-plugin-pwa + Workbox (FR) |
| [https://developer.chrome.com/docs/workbox](https://developer.chrome.com/docs/workbox)                                     | Guides Workbox officiels            |
| [https://v2.tauri.app/](https://v2.tauri.app/)                                                                             | Alternative légère à Electron       |
| [https://nativescript.org/](https://nativescript.org/)                                                                     | Docs NativeScript                   |
| [https://lynxjs.org/](https://lynxjs.org/)                                                                                 | Projet Lynx                         |
| [https://reactnative.dev/docs/dimensions](https://reactnative.dev/docs/dimensions)                                         | API Dimensions RN                   |
| [https://reactnavigation.org/docs/getting-started](https://reactnavigation.org/docs/getting-started)                       | React Navigation                    |
| [https://docs.expo.dev/versions/latest/sdk/bar-code-scanner/](https://docs.expo.dev/versions/latest/sdk/bar-code-scanner/) | Expo BarCodeScanner                 |
| [https://mobx.js.org/](https://mobx.js.org/)                                                                               | Docs MobX                           |
| [https://zustand-demo.pmnd.rs/](https://zustand-demo.pmnd.rs/)                                                             | Playground Zustand                  |
| [https://developer.mozilla.org/fr/docs/WebAssembly](https://developer.mozilla.org/fr/docs/WebAssembly)                     | Référence WASM                      |
| [https://www.tensorflow.org/js](https://www.tensorflow.org/js)                                                             | TensorFlow\.js                      |
| [https://api-adresse.data.gouv.fr/](https://api-adresse.data.gouv.fr/)                                                     | API Adresse Gouv                    |

---

## 9. Cheat‑sheets essentielles

### 9.1 PWA Quickstart

```bash
npm init vite@latest my‑pwa
cd my‑pwa
npm install
npm install -D vite-plugin-pwa
```

`vite.config.ts`

```ts
plugins: [VitePWA({ registerType: 'autoUpdate' })]
```

### 9.2 React — Composant basique

```tsx
function Hello({ name }: { name: string }) {
  return <h1>Hello {name}</h1>;
}
```

### 9.3 React Native — Flexbox

| Propriété        | Valeurs            |            |                  |
| ---------------- | ------------------ | ---------- | ---------------- |
| `flexDirection`  | `column` (défaut)  |  `row`     |                  |
| `justifyContent` | `flex-start`       |  `center`  |  `space-between` |
| `alignItems`     | `stretch`          |  `center`  |  `flex-end`      |

### 9.4 Throttle vs Debounce (Lodash)

```ts
import { throttle, debounce } from 'lodash-es';
const onScroll = throttle(handleScroll, 200);
const onSearch = debounce(handleSearch, 300);

```


### Où se place **Expo** ? — différence entre **PWA** et « Hybride »

| Catégorie            | Exemple concret                                  | Comment ça tourne ?                                                                                                   | Installation Store ? | Accès matériel (caméra, GPS…) | Perf. générale |
|----------------------|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------------------|-------------------------------|----------------|
| **PWA**             | Site web + *service-worker* (`vite-plugin-pwa`, Workbox…) | Code **HTML/CSS/JS** exécuté dans le **navigateur / une WebView** (Chrome, Safari mobile).                            | ❌ (sauf mini-wrapper) | **Limité** (APIs web)         | ⚪️⚪️⚪️ |
| **Hybride / Bridge** | React Native **+ Expo**, Flutter, NativeScript, Lynx | JS (ou Dart) tourne dans un moteur → envoie des ordres au **système natif** pour dessiner de **vrais widgets**.        | ✅ (APK / IPA)        | **Élevé** (modules natifs)     | ⚪️⚪️⚫️ |
| **100 % natif**      | Swift UI, Kotlin / Jetpack Compose               | Tout est écrit directement dans le langage de la plateforme.                                                          | ✅                    | **Complet**                   | ⚫️⚫️⚫️ |

---

#### 1. PWA  
- **Toujours du web** : HTML, CSS, JavaScript + _service-worker_.  
- **Avantages** : un seul déploiement, URL partageable, budget mini.  
- **Limites** : APIs matérielles restreintes (Bluetooth, NFC complet, capteurs précis…) et performances graphiques moindres.

#### 2. Hybride (Bridge)  
- **React Native** appartient à cette catégorie : ton JS décrit l’UI, le *bridge* la *traduit* en widgets iOS/Android.  
- **Expo** n’est **pas** une PWA ; c’est une **boîte à outils** qui simplifie React Native :  
  - création de projet, *hot-reload*, QR-code pour tester, build cloud ;  
  - modules prêts : caméra, notifications, biométrie…  
- Produit final : un **vrai binaire** (APK/IPA) publié sur les Stores.

#### 3. Natif pur  
- Code écrit en **Swift** (iOS) ou **Kotlin** (Android).  
- **+** : performances maximales, contrôle total.  
- **−** : deux code-bases, coût et maintenance plus élevés.

> **À retenir**  
> - **Expo = React Native amélioré ⇒ catégorie “Hybride”, pas PWA.**  
> - Une **PWA** reste un site web “dopé” (manifest + service-worker).  
> - Choix = compromis entre budget, performances et accès matériel.

---

### Manifest : c’est quoi ?  
Le **_web app manifest_** est un fichier JSON (souvent `manifest.webmanifest` ou `manifest.json`) déclaré dans le `<head>` d’une PWA :

```html
<link rel="manifest" href="/manifest.webmanifest" />
```
Il décrit à votre navigateur & au système :

Clé	Rôle
name, short_name	Nom complet et nom court de l’app (pour l’icône d’accueil).
icons	Tableau d’icônes (png/svg) tailles variées.
start_url	URL à ouvrir au lancement depuis l’icône.
display	standalone, fullscreen, minimal-ui …
theme_color	Couleur de la barre d’état / splash screen.
background_color	Couleur du splash avant le premier rendu.

En bref, le manifest dit : « Quand l’utilisateur installe ma PWA, voici le nom, l’icône et la façon dont je veux apparaître. »

## 3.x  Communiquer **Parent ⇄ Enfant** en React  
*(“Donner le pouvoir et recevoir des nouvelles”)*

### 🌳 Métaphore : l’arbre, la gourde et le talkie-walkie  

1. **L’arbre** : chaque composant est une branche ; le *Parent* est au-dessus, l’*Enfant* pend en dessous.  
2. **La gourde** (*props*) : le parent fait passer **des données** vers le bas ; l’enfant boit mais **ne peut pas la remplir** (lecture seule).  
3. **Le talkie-walkie** (*callback*) : pour parler **du bas vers le haut**, le parent prête un talkie-walkie (une fonction).  
   L’enfant appuie sur le bouton ⇒ le parent reçoit le message et agit.

---

### 🛠️  Recette pas à pas

| Étape | Côté parent                                              | Côté enfant                          |
|-------|----------------------------------------------------------|--------------------------------------|
| **1. État**          | Stocke une valeur avec `useState`.              | —                                    |
| **2. Prop (donnée)** | Passe la valeur (`count`) à l’enfant.           | Lit `props.count`.                   |
| **3. Prop (fonction)** | Crée un handler `handleIncrement` et le **passe**. | Appelle `props.onIncrement()` lors d’un événement. |
| **4. Réaction**      | Le handler met à jour l’état ⇒ tout l’arbre se re-rend. | —                                    |

---

### 🔍 Exemple concret

```tsx
// Parent.tsx
import { useState } from 'react';
import ChildCounter from './ChildCounter';

export default function Parent() {
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount(c => c + 1);

  return (
    <div>
      <h2>Parent count: {count}</h2>
      <ChildCounter
        count={count}
        onIncrement={handleIncrement}
      />
    </div>
  );
}
```
```tsx
// ChildCounter.tsx
type Props = {
  count: number;
  onIncrement: () => void;
};

export default function ChildCounter({ count, onIncrement }: Props) {
  return (
    <button onClick={onIncrement}>
      Child count (read-only): {count}
    </button>
  );
}
```
Ce qu’il se passe :

Le parent donne count (la gourde) et onIncrement (le talkie-walkie).

L’enfant affiche count.

Au clic, l’enfant parle via onIncrement.

Le parent met à jour son état ⇒ il redescend la nouvelle valeur ; l’enfant se re-rend automatiquement.

⚠️ Pièges classiques
Mauvaise idée	Pourquoi ?	Alternative
Modifier props.count directement dans l’enfant	Les props sont immutables	Demander au parent via onIncrement.
Passer un objet/fonction recréé à chaque rendu	L’enfant croit que la prop change	Utiliser useCallback / useMemo dans le parent.
Dupliquer le même état dans plusieurs composants	Risque d’incohérence	Centraliser l’état le plus haut possible.

🧠 À retenir
Flux unidirectionnel
Données ↘ vers le bas (props), événements ↗ vers le haut (callbacks).

Les props sont comme des ingrédients : on les reçoit prêts à l’emploi,
on ne les cuisine pas dans l’assiette de l’autre.

Pour “remonter” une info, on appelle la fonction fournie par le parent.

Si la donnée doit être partagée par plusieurs branches sans passer par tous les intermédiaires,
utiliser Context ou un store (Zustand, Redux…).

# Mobile hybride

## Jour 1

PWA : progresive webapp abjectif d'avoir un site adapter au mobile
React + PWA alors qu'on maitrise totalement Angular. En mobile moins de debat pour le mobile IOS c'est un mac c'est le seul OS qui permet de developer du mobile. Pour le dev en genrale on peut utiliser windox, linux... pas de preference. 
De meme pour les framework JS, pareil chacun à ses avantages et inconvenients. React est le framework le plus utiliser dans le monde du dev mbile hybride. Historiquement grosse dif entre je fais du mobile avec react native (couche abstraction perf ok); ou le choix react native script c'est un peu comme du electron qui permet de lancer l'application (voir les def). Modulo Lynx peut etre un concurent de react natif potentiel.



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

SafeAreaView : bord arrrondi qui ne sont pas safe, une zone non accessible a ne pas developpé sur ecran

ScrollView : utiliser les bon outils

Platform : IOS ou Android if c'est IOS ... else ... mettre dans son code le type de platform

Style CSS : utiliser les bon outils pour avoir le style dans un mobile (pas talwind) on va tester vanilla

Pas hover mais des drag and drop

on va plus ecrire des div mais des views dans les balises quelque specificité mais ressemble à ce qu'on fait d'habitude


connaitre le choix expo qui est centralisé un peu comme next on ne passe plus par react native.

Pour etre propre dans le code on utilise expo
npx create-expo-app@latest
ajouter au start --tunel
"start": "expo start --tunnel",
safeareaview: est fournit par le constructeur. : https://docs.expo.dev/develop/user-interface/safe-areas/
Le safeareaview ne fonctionne plus a ce jour il faut donc utiliser un autre moyen avec provider:

Entouré toute l'application d'un provider :
https://appandflow.github.io/react-native-safe-area-context/api/use-safe-area-insets

insets : ecart qu'il a par raport à la droite en haut et en bas et on ajoute des padding : 

```ts
import { useSafeAreaInsets } from 'react-native-safe-area-context';

function HookComponent() {
  const insets = useSafeAreaInsets();

  return <View style={{ paddingBottom: Math.max(insets.bottom, 16) }} />;
}

```

Contexte en react a quoi ca sert : on revient sur l'histoire des parents a un enfant donc comment communiquer. Mais quand on part d'un parent a un ariere ariere petit enfant il faut faire des petits pont. 
Ce qu'on peut faire c'est que le parent possede de superpouvoir et ainsi il donnera le pouvoir au enfant reducts exemple -->
ce qui adore faire des classe mobx cas Angular Rjxx a voir https://mobx.js.org/README.html

revoir un observable definition.



https://zustand-demo.pmnd.rs/

dans l'outil on lui envoie tout les elements qu'on souhaite modifier. on garde la logique dans un composent si par contre il a des impacts sur les autres composant on extrait ceci pour pouvoir communiquer de parent a enfant 


Meme chose que pour les outils zustand et les classes on utilse contexte afin de communiquer entre parent component et enfant: 
https://react.dev/reference/react/useContext
on export mon contexte que j'ai creer et on l'utilise de tel maniere : 

```ts
import { useContext } from 'react';

function Button() {
  const theme = useContext(ThemeContext);
```

```ts
import { createContext, useContext } from 'react';

const ThemeContext = createContext(null);

export default function MyApp() {
  return (
    <ThemeContext value="dark">
      <Form />
    </ThemeContext>
  )
}

function Form() {
  return (
    <Panel title="Welcome">
      <Button>Sign up</Button>
      <Button>Log in</Button>
    </Panel>
  );
}

function Panel({ title, children }) {
  const theme = useContext(ThemeContext);
  const className = 'panel-' + theme;
  return (
    <section className={className}>
      <h1>{title}</h1>
      {children}
    </section>
  )
}

function Button({ children }) {
  const theme = useContext(ThemeContext);
  const className = 'button-' + theme;
  return (
    <button className={className}>
      {children}
    </button>
  );
}
```

Lorsqu'on va utilise SafeAreaProvider c'est une view qui va donc fournir à tous ses enfants.

SafeAreaView a voir si ca focntionne
useSafeAreaInsets 

https://react.dev/reference/react/useReducer

https://developer.mozilla.org/fr/docs/WebAssembly

https://www.tensorflow.org/?hl=fr


demander le package.json dans la recherche de travail si react + autre stack apolo voir les version à demander avant les entretiens


On est dans une logique contexte
provider 

# Cours : Le **Context** dans React

## 1. Pourquoi le Context ?

### 1.1 Le problème : « prop‑drilling »

* Dans React, les données voyagent **du parent vers les enfants** via les props.
* Lorsque vous devez transmettre la même donnée à un **arrière‑arrière‑petit‑enfant**, chaque composant intermédiaire ne fait que relayer la prop.
* Résultat : code verbeux, fragile, difficile à maintenir.

### 1.2 La solution : un “super‑pouvoir” partagé

* **Context** vous permet de créer un **magasin de valeurs** (thème, utilisateur, langue, etc.) que **tous** les descendants du *Provider* peuvent consommer sans intermédiaires.
* Imaginez un parent qui **partage directement** son pouvoir à n’importe quel enfant de l’arbre.

---

## 2. Mise en place rapide

```tsx
import { createContext, useContext } from 'react';

const ThemeContext = createContext<'light' | 'dark'>('light');

export default function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Form />
    </ThemeContext.Provider>
  );
}

function Form() {
  return (
    <Panel title="Bienvenue">
      <Button>S’inscrire</Button>
      <Button>Se connecter</Button>
    </Panel>
  );
}

function Panel({ title, children }: { title: string; children: React.ReactNode }) {
  const theme = useContext(ThemeContext);       // <-- consommation
  return (
    <section className={`panel-${theme}`}>
      <h1>{title}</h1>
      {children}
    </section>
  );
}

function Button({ children }: { children: React.ReactNode }) {
  const theme = useContext(ThemeContext);       // <-- consommation
  return <button className={`button-${theme}`}>{children}</button>;
}
```

> **Étapes :**
>
> 1. `createContext` crée le conteneur.
> 2. Le **Provider** place la valeur dans l’arbre.
> 3. `useContext` la récupère à n’importe quel niveau.

---

## 3. Quand **ne pas** utiliser Context ?

| Besoin                                            | Recommandation                                                 |
| ------------------------------------------------- | -------------------------------------------------------------- |
| Valeur utilisée **partout** (thème, langue, auth) | **OK** pour Context                                            |
| **État local** à 2‑3 niveaux                      | Rester sur des **props**                                       |
| **État complexe** partagé par plusieurs pages     | Envisager **Zustand**, **Redux Toolkit**, **Jotai**, **MobX**… |

---

## 4. Context & autres outils d’état

### 4.1 MobX / RxJS (Angular)

* **MobX** : magasin *observable* ; un composant réagit aux variables qu’il **utilise réellement**.
* **RxJS** : flux d’`Observable` (async, streams) – populaire dans Angular.
* Combinez Context + MobX : exposez votre store MobX dans un Context pour garder l’API React simple.

### 4.2 Zustands

* **Zustand** (allemand : « état ») est un **micro‑store** minimaliste.

```ts
import { create } from 'zustand';

const useBearStore = create(set => ({
  bears: 0,
  addBear: () => set(state => ({ bears: state.bears + 1 }))
}));
```

* Pas besoin de Context : `useBearStore()` fonctionne n’importe où dans l’arbre, mais vous pouvez l’isoler derrière un Context si vous voulez.

---

## 5. Context avancé

### 5.1 Combiner avec `useReducer`

```ts
const FormContext = createContext(null);

function FormProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <FormContext.Provider value={{ state, dispatch }}>
      {children}
    </FormContext.Provider>
  );
}
```

* On obtient un **dispatcher** façon Redux mais **sans dépendance externe**.

### 5.2 Context dans React Native

```ts
import { SafeAreaProvider, useSafeAreaInsets } from 'react-native-safe-area-context';

export default function App() {
  return (
    <SafeAreaProvider>
      <MyScreen />
    </SafeAreaProvider>
  );
}

function MyScreen() {
  const { top } = useSafeAreaInsets();
  return <View style={{ paddingTop: top }} />;
}
```

* **SafeAreaProvider** expose les `insets` d’écran (encoches, Dynamic Island…) via Context.
* **SafeAreaView** est un wrapper pratique qui **consomme** ce Context pour appliquer le padding automatique.

---

## 6. Bonnes pratiques

1. **Un Context par souci** (Theme, Auth, Locale…).
2. Évitez d’y stocker des valeurs qui **changent à chaque rendu** (fonctions anonymes, objets recréés) ; mémoïsez‑les (`useMemo`, `useCallback`) ou passez un **réducteur**.
3. **Versionnez vos dépendances** : avant un entretien, ouvrez `package.json`/`pnpm-lock.yaml`/`yarn.lock` pour vérifier :

   * `react`, `react-dom`, `react-native`.
   * Outils d’état : `@tanstack/react-query`, `zustand`, `redux-toolkit`, `mobx`…
   * GraphQL : `@apollo/client` (v3 → hooks, v4 → suspense)…
   * TypeScript, ESLint, tooling (Vite, Next.js 15, Expo 50, etc.).

---

## 7. Pour aller plus loin

| Sujet                       | Pour quoi faire ?                                                                                    |
| --------------------------- | ---------------------------------------------------------------------------------------------------- |
| **WebAssembly**             | Exécuter du code C/Rust/Go dans le navigateur (perf, FFT, encodage).                                 |
| **TensorFlow\.js**          | Charger un modèle ML et l’inférer côté client ou React Native.                                       |
| **React Server Components** | Réduire le JS envoyé au client ; parfois remplace certains Context globaux par un **cache serveur**. |

---

## 8. Récapitulatif

* **Context** résout le **prop‑drilling** : partage d’une valeur à tout un sous‑arbre.
* Pour de l’état **très transversal** ou **persistant**, préférez un **store dédié** (Zustand, Redux, MobX).
* En React Native, beaucoup de libs (SafeAreaProvider, GestureHandler) reposent sur Context pour injecter des infos système.
* Combinez‑le intelligemment avec `useReducer`, des **observables** ou un **micro‑store** pour garder un code clair et scalable.

---

> **TL;DR** : « Quand c’est un **super‑pouvoir** dont tous les descendants ont besoin → **Context**. Quand c’est l’état interne d’un composant → **props/état local**. Quand c’est l’état global de l’application → **store dédié**. »


https://reactnative.dev/docs/dimensions


https://reactnavigation.org/docs/getting-started

https://docs.expo.dev/versions/v51.0.0/sdk/bar-code-scanner/


on demarre au debuut avec l'envie de partir sur du web
on bascule sur mobile pour les maps
lorsqu'on passe au dessus on perd des couts...

Pourquoi passer au mobile
performance (jeu, etc...) a prendre en compte quand on passe au mobile
nouveauté eco systeme smart watch, casque vr, lunette connecté 

### 6.x  **Workers, Service Workers & stratégies de cache — l’essentiel**

#### 👷‍♂️ 1. “Worker” ≠ “Service Worker”  

| Terme                | Où ça tourne ?                          | À quoi ça sert ?                                                                                     | Exemple concret |
|----------------------|-----------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------|
| **Web Worker**       | Thread JS **secondaire** (page ouverte) | Parcourir un gros JSON, encoder une vidéo, entraîner un mini-ML **sans bloquer l’UI**.               | Calcul d’un aperçu vidéo pendant que l’utilisateur clique. |
| **Service Worker**   | Thread JS **hors page** (proxy réseau)  | Intercepter requêtes, gérer **cache**, **offline**, **push**, **background sync** même appli fermée. | Notif “nouveau message” + synchro des brouillons dès réseau. |

> Pense-le comme **un majordome : toujours là, même si la porte (l’onglet) est fermée.**

---

#### 🔔 2. Capacités du _service worker_ (SW)

| Capacité SW                | Description rapide | Sources |
|----------------------------|--------------------|---------|
| **Push Notifications**     | Réveille le SW à la réception d’un message push → affiche une notif, réveille l’app. | :contentReference[oaicite:0]{index=0} |
| **Background Sync**        | Si réseau coupé, le SW enregistre la tâche ; dès la reconnection il la rejoue.        | :contentReference[oaicite:1]{index=1} |
| **Periodic Sync / Cron**   | API (encore limitée) pour lancer un fetch à heure fixe (ex. météo quotidienne).       | :contentReference[oaicite:2]{index=2} |
| **Proxy réseau + Cache**   | Agit comme un proxy programmable ; choisit d’aller au cache, au réseau ou les deux.   | :contentReference[oaicite:3]{index=3} |

Exemples d’apps fermées mais actives : podomètre (pas + envoi serveur), app mail qui pré-télécharge vos messages.

---

#### 🗄️ 3. Stratégies de cache Workbox (résumé “anti-trou noir”)  

| Stratégie Workbox                  | Flux décisionnel                                     | Quand l’utiliser ?                                      | Avantages / Limites | Sources |
|------------------------------------|------------------------------------------------------|---------------------------------------------------------|---------------------|---------|
| **CacheOnly**                      | Toujours le cache → **jamais** réseau                | Assets *précachés* qui ne changent pas (ex : logo v123).| Ultra rapide / **jamais** mis à jour | :contentReference[oaicite:4]{index=4} |
| **NetworkOnly**                    | Toujours le réseau                                   | Données **temps réel** : météo, bourse.                | Fresh / Offline KO  | :contentReference[oaicite:5]{index=5} |
| **CacheFirst**                     | Si cache dispo → renvoie, sinon réseau + mise en cache | Polices, images versionnées.                           | Faible latence / risque stale | :contentReference[oaicite:6]{index=6} |
| **NetworkFirst**                   | Tente réseau, fallback cache si offline              | Docs éditables, agenda : on préfère la fraîcheur.       | Offline OK / premier chargement ↗ | :contentReference[oaicite:7]{index=7} |
| **StaleWhileRevalidate**           | Sert **immédiat** le cache, MAJ en arrière-plan      | Blogs, listes produits : UX rapide + cache actualisé.   | Mix perf / 2 requêtes | :contentReference[oaicite:8]{index=8} |

> **Mnemonic** • “Cache First = Vitesse” • “Network First = Fraîcheur” • “StaleWhileRevalidate = Meilleur des deux mondes”.

---