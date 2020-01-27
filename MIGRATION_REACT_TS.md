---
marp: true
title: Migrer progressivement vos app React en TS
description: Migrer progressivement vos app React en TS
theme: uncover
paginate: true
_paginate: false
---

![bg](./assets/gradient.jpg)

# <!--fit--> Migrer vos app React en Typescript

REX

https://github.com/yhatt/marp-cli-example

<style scoped>a { color: #eee; }</style>

<!-- Ca y est vous vous êtes décidé, on va passer à Typescript. Ca fait longtemps que ça tourne, les autres ont essuyé les pots cassés), le tooling devient à peu près au point. Bon, sauf qu'expliquer qu'on va passer 2 mois à réécrire tout le code existant, c'est pas vraiment faisable.

Il y a beaucoup de literature sur le “comment” migrer du Javascript vers Typescript,
ce talk est un retour d'experience sur la migration progressive des nos applications Reac, par où on a commencé, comment faire cohabiter du code legacy et du typescript, s'assurer que le code transpilé soit le même et tirer parti des bénéfices immédiats. -->

---

## Setup

---

### Configuration 

- Webpack
- Jest
- Babel ?

- Lint ?

---

### Typechecking

Effectuer le typechecking dans un process séparé 

https://github.com/TypeStrong/fork-ts-checker-webpack-plugin



<!-- Tip: utiliser un plugin séparé pour réaliser le type checking . En dev, c’est vraiment plus rapide.  -->


---

### Strategies

---

#### En douce 

Utiliser des fichiers d.ts

https://devblogs.microsoft.com/typescript/how-to-upgrade-to-typescript-without-anybody-noticing-part-2/





---

##### Declaration Files 

<!--  MEttre ici un exemple de fichier de déclaration-->

![Marp bg 60%](https://raw.githubusercontent.com/marp-team/marp/master/marp.png)
