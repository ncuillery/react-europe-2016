# react-europe-2016

## Intro



## Keynote: The Redux journey



## Native Navigation for Every Platform



## A cartoon guide to performance in React



## React Native <3 60FPS -- Improving React Native animations



## Being Successful at Open Source



## GraphQL at Facebook



## A Deepdive Into Flow

Nous sommes prévenu d'entrée de jeu, le talk qui va suivre est très technique et nécessitera sans doute une revue de la vidéo 
pour bien le comprendre. Jeff Morrison nous a présenté comment fonctionne Flow sous le capot, en quoi il se différencie des 
autres _type checkers_, et à quoi Flow peut servir au delà du _type checking_.

Le workflow de Flow (!) est divisé en 2 étapes: l'[inférence](https://fr.wikipedia.org/wiki/Inf%C3%A9rence_de_types) suivi de l'évaluation. Jeff choisit ces 2 lignes de code pour décrire ce qui se passe:

```javascript
var a = "abcd";
a.lenght // Typo volontaire
```

### Inférence

Cette phase consiste en la lecture de l'arbre syntaxique (AST) issue de ce code. Le premier type qui en est tiré est un type ouvert 
"**OpenT**" provenant de la simple déclaration de `a`. En effet, un simple `var a;` ne laisse rien présager de la nature de la
variable.
Sur la même ligne nous avons également `"abcd"` qui débouche logiquement sur un type "**StringT**". L'opération d'affectation 
débouche sur une liaison appellée "flow constraint" entre ces 2 types. Sémantiquement, on dit que le type **StringT** "coule" 
dans le type **OpenT** (_flow into_ en anglais, d'où le nom de l'outil).
Enfin, la deuxième ligne se traduit par un `GetPropT`. Fait intéressant : la notion de type dans Flow ne se limite pas seulement aux 
types à proprement parler mais également aux "actions" (ici : accès à une propriété d'un objet). La liaison entre `a` et sa 
propriété (matérialisé par le point de `a.lenght`) aboutit également à une __flow constraint__ : le type **OpenT** de `a` "coule" 
dans le type `GetPropT`.
En sortie, nous avons un graphe appelé _Flow graph_ qui est une représentation de l'intégralité des variables et de leurs interactions. Pour l'exemple donné, il se résume à `StringT --> OpenT --> GetPropT`.




## Debugging flux applications in production



## On the Spectrum of Abstraction



## React Redux Analytics



## Evolving the Visual Programming Environment with React



## React Native Retrospective



## The Evolution of React UI Development



## Recomposing your React application



## JavaScript, React Native and Performance



## Falcor: One Model Everywhere



## Building li.st for Android with Exponent and React Native



## GraphQL Future



## Building native mobile apps with GraphQL



## Conclusion



