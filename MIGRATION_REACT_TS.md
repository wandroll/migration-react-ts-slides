---
marp: true
title: Migrer progressivement vos app React en TS
description: Migrer progressivement vos app React en TS
theme: gaia
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
![bg right](https://picsum.photos/720?image=3)

### Wandrille VERLUT

Front-End Developer @iAdvize

@Wverlut


<!-- Qui suis je ? -->
---

---

### Configuration 

- Webpack
- Jest
- Babel ?

- Lint ?

---

### Typechecking

Effectuer le typechecking dans un process séparé avec  fork-ts-checker-webpack-plugin

https://github.com/TypeStrong/fork-ts-checker-webpack-plugin


-> plus rapide surtout en dévelopement
<!-- Tip: utiliser un plugin séparé pour réaliser le type checking . En dev, c’est vraiment plus rapide.  -->

---

### Linting

- TsLint : bientot déprécié 
- ESLint 

````json
// .eslintrc

{
  "parser": "@typescript-eslint/parser",

}
````

###### https://github.com/palantir/tslint/issues/4534
<!-- TSlint va etre bientot déprécié
et d'ailleurs typescript-eslint-parser aussi 
C'est le projet typescript-eslint pour la 
--->

---

# Strategies

---

#### En douce 

Utiliser des fichiers d.ts

https://devblogs.microsoft.com/typescript/how-to-upgrade-to-typescript-without-anybody-noticing-part-2/


--- 

### En douceur

On a commencé par l’exterieur:
-  nos call API, 
puis les services metier, 
- la logique redux ( store et action), les sagas, 
- enfin les composants.


---

##### Declaration Files 

<!--  MEttre ici un exemple de fichier de déclaration-->

![Marp bg 60%](https://raw.githubusercontent.com/marp-team/marp/master/marp.png)



---

#### Quelques TIPS de migration


---

##### Les Enums


````ts

export const PostCategories = {
  Immobilier: 'Immobilier',
  BonnesAffaires: 'BonnesAffaires',
  Sport: 'Sport',
  Vetements: 'Vetements',
} as const;


enum PostCategoryEnum {
    'Immobilier',
    'BonnesAffaires',
    'Sport',
    'Vetements',
}


export type Valueof<T> = T[keyof T];

export type PostCategoriesEnum = Valueof<typeof PostCategories>

const aCategory: PostCategoriesEnum = 'Vetement';

`````

````js

var PostCategoryEnum;
(function (PostCategoryEnum) {
    PostCategoryEnum[PostCategoryEnum["Immobilier"] = 0] = "Immobilier";
    PostCategoryEnum[PostCategoryEnum["BonnesAffaires"] = 1] = "BonnesAffaires";
    PostCategoryEnum[PostCategoryEnum["Sport"] = 2] = "Sport";
    PostCategoryEnum[PostCategoryEnum["Vetements"] = 3] = "Vetements";
})(PostCategoryEnum || (PostCategoryEnum = {}));
export var PostCategories = {
    Immobilier: 'Immobilier',
    BonnesAffaires: 'BonnesAffaires',
    Sport: 'Sport',
    Vetements: 'Vetements',
};
var aCategory = 'Vetement';
````

--- 

### Les Assertions

````ts

interface Foo {
bar: number;
bas: string;
}

var foo = {} as Foo;   // bouhhouuuu

var foo = <Foo>{}; // juste l'autocomplétion
// better
var foo:Foo = {}; // autocomplete + complete typechecking
````

--- 

#### Migration de Composants

<!-- Typer des composants implique de dédier pas mal de temps à la compréhension de certains concept avancés nottament les types génériques et la composition de type 
-->


---

##### Typescript vs PropTypes

<!--  Le typage de ProptType est vraiment insuffisant. Par exemple   `optionalFunc: PropTypes.func,`  c’est pas très explicite en terme de paramètres attendu et retour

Le plus : ça pete à la comipile et on peut virer propTypes
Le moins : on enleve les props types donc ça ne pete plus d’anomalie au runtime … 
--->