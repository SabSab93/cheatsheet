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
Copier
Modifier
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

🧠 À retenir “pour l’oral”
Flux unidirectionnel
Données ↘ vers le bas (props), événements ↗ vers le haut (callbacks).

Les props sont comme des ingrédients : on les reçoit prêts à l’emploi,
on ne les cuisine pas dans l’assiette de l’autre.

Pour “remonter” une info, on appelle la fonction fournie par le parent.

Si la donnée doit être partagée par plusieurs branches sans passer par tous les intermédiaires,
utiliser Context ou un store (Zustand, Redux…).

