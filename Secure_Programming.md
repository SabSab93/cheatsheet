# Secure Programming

pour etre un bon cybersecurity il faut etre bon en dev, bon en reseau, en archi

Botnet: voir l'exemple du telephone

WAF ?
creation de plans de reponse aux incidents : honey


analyse statique de code a mettre des le debut de notre code : exemple sonarqube et sonarcloud

https://letsencrypt.org/fr/ à voir et passer par la pour securiser le code
pas de deouble authe avec sms car risque de spoof

```ts
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import { Clerk } from "@clerk/clerk-js";

createApp(App).mount('#app')

const clerkPubKey = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY as string

const clerk = new Clerk(clerkPubKey)
await clerk.load()

const appElement = document.getElementById('app')

if (!appElement) {
  console.error("Element with id 'app' not found")
} else {
  if (clerk.user) {
    appElement.innerHTML = `
      <div id="user-button"></div>
    `
    const userButtonDiv = document.getElementById('user-button')
    if (userButtonDiv) {
     
      clerk.mountUserButton(userButtonDiv as HTMLDivElement)
    }
  } else {
    appElement.innerHTML = `
      <div id="sign-in"></div>
    `
    const signInDiv = document.getElementById('sign-in')
    if (signInDiv) {
      clerk.mountSignIn(signInDiv as HTMLDivElement)
    }
  }
}
```

