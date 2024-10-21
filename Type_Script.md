```typescript
// NE PAS TOUCHER
const values: number[] = [4, 3, 6, 7, 8, 7, 3, 4, 6, 4, 5, 1, 7, 5, 4, 8, 10, 1, 5, 6, 1, 7, 2, 2];
// NE PAS TOUCHER

let sum =0
values.forEach ((value, index) =>{
    sum = sum + index
})

const doubleValues = values.map ((value, index) =>{
    return value
})

const findValues = values.find ((value, index) =>{
    return value.lenght >2
})


console.log(doubleValues)

const findValues = values.filter ((value, index) =>{
    return value.length >1
})

```
Notion de split pour creer un tableau à partir d'une chaine de caractere

Tableau de code ascii

```typescript

const tata ="tata"


```
https://www.ascii-code.com/fr

```typescript
const tata ="tata"

const splittedTata =tata.split("")
const splittedCeaser = splittedTata.map (
    (val,i)=> {
        const pos = val.charCodeAt(0)
        return String.fromCharCode(pos +2)
    }
)

const res = splittedCeaser.join("")
```

probleme si on prend la lettre z ça va se decaler et prendre un caractere -> utilisation du modulo (division euclidienne)

```typescript
const tata ="tata"

const splittedTata =tata.split("")
const splittedCeaser = splittedTata.map (
    (val,i)=> {
        const pos = val.charCodeAt(0)
        return 97 - (String.fromCharCode(pos +2)%32)
    }
)

const res = splittedCeaser.join("")
```

attention à la code review voir le cas sur coupe du monde de rugby 1
```typescript
// NE PAS TOUCHER
const line1: string[] = ["111:91", "115:35", "100:35"];
const line2: string[] = ["93:91", "89:87", "110:97", "109:72"];
const line3: string[] = ["97:10"];
// NE PAS TOUCHER

function getImpact(line: string[], facteur: number = 1){
    let impactTotale = 0
    line.forEach(joueur => {
        /* cas qui peut etre remplacé
        const split = joueur.split(":")
        const poidsStr = split[0]
        const forceStr = split[1]
        */
        const [poidsStr, forceStr] = joueur.split(":")
        const force = parseInt(poidsStr) * parseInt(forceStr)
        impactTotale += force
    })
    return Math.floor (forceTotale * facteur)
}

const forceline1= getImpact(line1,1.5)
const forceline2= getImpact(line2)
const forceline3= getImpact(line3,0.75)

const res = forceline1 + forceline2 + forceline3
console.log(res)

```
code review
je comprends pas / code critique / propreté du code

le concept du dry : don't repeat yourself

revoir map / filter / reduce 

cas avec reduce 

```typescript
// NE PAS TOUCHER
const line1: string[] = ["111:91", "115:35", "100:35"];
const line2: string[] = ["93:91", "89:87", "110:97", "109:72"];
const line3: string[] = ["97:10"];
// NE PAS TOUCHER

function getImpact(line: string[], facteur = 1){
    const impactTotale = line.reduce((sum, joueur, i) => {
        const [poidsStr, forceStr] = joueur.split(":")
        const force = parseInt(poidsStr) * parseInt(forceStr)
 
        return sum + force
    }, 0)
    return Math.floor(impactTotale * facteur)
}
 
const forceLine1 =  getImpact(line1, 1.5)
const forceLine2 = getImpact(line2)
const forceLine3 = getImpact(line3, 0.75)
 
const res = forceLine1 + forceLine2 + forceLine3
 
console.log(res)

```


