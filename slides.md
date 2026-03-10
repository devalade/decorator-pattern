---
theme: seriph
title: Decorator Pattern
info: |
  ## Decorator Pattern
  Ajouter des fonctionnalités dynamiquement sans modifier le code existant
class: text-center
drawings:
  persist: false
transition: slide-left
duration: 5min
---

# Decorator Pattern

## ☕ Comment ajouter du lait ET du sucre à un café
## **sans créer 50 classes ?**

<div @click="$slidev.nav.next" class="mt-12 py-1 cursor-pointer" hover:bg="white op-10">
  <carbon:arrow-right /> Commencer
</div>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
transition: slide-up
class: text-center
---

# L'Analogie du Café ☕

<div v-click class="mt-8">
  <CoffeeVisualizer />
</div>

<div v-click class="mt-8 text-xl">
  Chaque décorateur <strong>enveloppe</strong> le précédent<br>
  et ajoute son propre comportement
</div>

---
transition: slide-left
---

# Le Problème : Héritage vs Composition

<div grid="~ cols-2 gap-8" class="mt-4">
<div v-click>

### ❌ Avec Héritage
```mermaid
graph TD
    A[Café] --> B[Café+Lait]
    A --> C[Café+Sucre]
    A --> D[Café+Chantilly]
    B --> E[Café+Lait+Sucre]
    B --> F[Café+Lait+Chantilly]
    C --> G[Café+Sucre+Chantilly]
    E --> H[Café+Lait+Sucre+Chantilly]
```

**Explosion combinatoire !** 💥

</div>
<div v-click>

### ✅ Avec Decorator
```mermaid
graph LR
    A[Café Simple] --> B[MilkDecorator]
    B --> C[SugarDecorator]
    C --> D[WhipDecorator]
```

**Composition flexible !** ✨

</div>
</div>

<div v-click class="mt-8 text-center text-xl">
  Le Decorator Pattern utilise la <strong>composition</strong>, pas l'héritage
</div>

---
transition: slide-up
layout: center
class: text-center
---

# La Mathématique derrière le Pattern

<div class="text-2xl">

<v-clicks>

<div class="mb-8">

**Fonction de base :**

$$f(x) = \text{Café à } 2€$$

</div>

<div class="mb-8">

**Décorateur Lait :**

$$g(x) = f(x) + 0.50€$$

</div>

<div class="mb-8">

**Décorateur Sucre :**

$$h(x) = g(x) + 0.30€$$

</div>

<div class="text-yellow-400 font-bold">

**Résultat :**

$$h(g(f(x))) = 2.80€$$

</div>

</v-clicks>

</div>

---
transition: slide-left
---

# Le Code Étape par Étape

<div class="text-left">

````md magic-move {lines: true}
```js
// Étape 1 : Classe de base
class Cafe {
  prix() { return 2 }
  nom() { return "Café" }
}

let c = new Cafe()
c.prix()  // → 2
```

```js
// Étape 2 : Premier décorateur
class Cafe {
  prix() { return 2 }
  nom() { return "Café" }
}

class Lait {
  constructor(cafe) {
    this.cafe = cafe
  }
  prix() { return this.cafe.prix() + 0.5 }
  nom() { return this.cafe.nom() + " + Lait" }
}

let c = new Cafe()
c = new Lait(c)
c.prix()  // → 2.5
c.nom()   // → "Café + Lait"
```

```js
// Étape 3 : On enchaîne !
class Cafe {
  prix() { return 2 }
  nom() { return "Café" }
}

class Lait {
  constructor(c) { this.c = c }
  prix() { return this.c.prix() + 0.5 }
  nom() { return this.c.nom() + " + Lait" }
}

class Sucre {
  constructor(c) { this.c = c }
  prix() { return this.c.prix() + 0.3 }
  nom() { return this.c.nom() + " + Sucre" }
}

let c = new Cafe()
c = new Lait(c)
c = new Sucre(c)
c.prix()  // → 2.8
c.nom()   // → "Café + Lait + Sucre"
```
````

</div>

---
transition: slide-up
---

# En Code Complet : Testez !

```ts {monaco-run}
class Cafe {
  prix() { return 2 }
  nom() { return "Café" }
}

class Lait {
  constructor(c) { this.c = c }
  prix() { return this.c.prix() + 0.5 }
  nom() { return this.c.nom() + " + Lait" }
}

class Sucre {
  constructor(c) { this.c = c }
  prix() { return this.c.prix() + 0.3 }
  nom() { return this.c.nom() + " + Sucre" }
}

let commande = new Cafe()
commande = new Lait(commande)
commande = new Sucre(commande)

console.log(commande.nom() + " = " + commande.prix() + "€")
```

---
transition: fade-out
class: text-center
---

# ✅ Points Clés à Retenir

<div class="grid grid-cols-3 gap-4 mt-12">

<div v-click>

### 🎯 **Principe**
$f(x) \rightarrow g(f(x)) \rightarrow h(g(f(x)))$

</div>

<div v-click>

### 🧱 **Structure**
Composition d'objets : chaque classe enveloppe la précédente

</div>

<div v-click>

### 🔀 **Ordre**
$h \circ g \circ f(x)$ — On peut composer dans n'importe quel ordre

</div>

</div>

<div v-click class="mt-16">

### 💡 Applications Réelles

- **Express.js** : `middleware3(middleware2(middleware1(req)))`
- **Node.js** : `compress(encrypt(readFile()))`
- **React** : `withAuth(withLogger(Component))`

</div>

---
layout: center
class: text-center
---

# Merci ! 🎉

## Questions ?

<style>
.slidev-layout {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  color: white;
}
</style>
