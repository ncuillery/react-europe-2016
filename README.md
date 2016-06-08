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
pour bien le comprendre ! Jeff Morrison nous a présenté comment fonctionne Flow sous le capot, en quoi il se différencie des 
autres _type checkers_, et à quoi Flow peut servir au delà du _type checking_.

Le workflow de Flow (!) est divisé en 2 étapes: l'[inférence](https://fr.wikipedia.org/wiki/Inf%C3%A9rence_de_types) suivi de l'évaluation. Jeff choisit ces 2 lignes de code pour décrire ce qui se passe:

```javascript
var a = "abcd";
a.lenght // Typo volontaire
```

### Inférence

Cette phase consiste en la lecture de l'arbre syntaxique (AST) issue de ce code.

- Le premier type qui en est tiré est un type ouvert "**OpenT**" provenant de la simple déclaration de `a`. En effet, un
simple `var a;` ne laisse rien présager de la nature de la variable.
- Sur la même ligne nous avons également `"abcd"` qui débouche logiquement sur un type "**StringT**". L'opération d'affectation 
entraîne une liaison appellée _Flow constraint_ entre ces 2 types. Sémantiquement, on dit que le type **StringT** "coule" 
dans le type **OpenT** (_flow into_ en anglais, d'où le nom de l'outil).
- Enfin, la deuxième ligne se traduit par un **GetPropT**. Fait intéressant : la notion de type dans Flow ne se limite pas
seulement aux types à proprement parler mais également aux "actions" (ici : accès à une propriété d'un objet). La liaison entre
`a` et sa propriété (matérialisé par le point de `a.lenght`) aboutit également à une __flow constraint__ : le type **OpenT** 
de `a` "coule" dans le type `GetPropT`.

En sortie, nous avons un graphe appelé _Flow graph_ qui est une représentation de l'intégralité des variables et de leurs
interactions. Pour l'exemple donné, il se résume à `StringT --> OpenT --> GetPropT`.

Face à cette apparente complexité, Jeff explique qu'à la différence des autres _type checkers_ statiques, Flow est pensé pour 
le JavaScript et son caractère dynamique. Afin d'illustrer son propos, il présente l'exemple suivant:

```javascript
var name = "Jeff";
name = name.toUpperCase(); // Ok
if (loggedOut) {
  name = null;
}
var firstInitial = name[0]; // Error!
```

Le _type checker_ lambda va détecter l'erreur à la ligne 4 arguant qu'on ne peut pas assigner `null` à un type String 
(_null-safe_) or il n'y a pas d'erreur à la ligne 4, il y en a une à la ligne 6. Et si on la corrige en faisant 
`name && name[0]`, il n'y a plus d'erreur du tout ! D'où la nécessité de tracker les variables tout au long du programme et 
lever des erreurs suivant leur utilisation.

A noter également, le graphe embarque également toutes les informations disponibles dans l'AST (valeur pour le **StringT**, 
nom de la propriété pour le **GetPropT**, ...), utile pour afficher des erreurs explicites.

### Evaluation

Une fois que l'AST a été complètement parsé, le graphe est parcouru en commençant par la racine (ici le **StringT**). Chaque 
_Flow constraint_ obéit à une règle différente selon les types reliés. Ces règles sont embarqués dans Flow. 

- Pour la première (**StringT** vers **OpenT**), la règle dit de supprimer l'**OpenT**, le **StringT** coule directement dans 
le **GetPropT**. Exactement comme si on avait écrit `"abcd".lenght` finalement.
- Pour la deuxième (**StringT** vers **GetPropT** donc), Flow se lance dans la recherche d'une propriété tout au long de la 
chaîne de prototype. Le type **GetPropT** est transformé en **LookupT** et le **StringT** est transformé en **InstanceT**
avec le name String (i.e. instance de String), ce type embarque aussi l'information de sa superclass (un **InstanceT 
"Object"**) et ses membres (`length`, `map()`, `forEach()`, etc.).
- La _flow constraint_ (devenue **InstanceT "String"** vers **LookupT**) effectue la recherche de la propriété parmis les 
membres du prototype qui se révèle infrutueuse (rappel: typo volontaire dans `lenght`). Le **InstanceT "String"** est remplacé
par celui de sa superclass.
- La _flow constraint_ part maintenant de **InstanceT "Object"** vers **LookupT**. Le scénario se répète (toujours pas de 
`lenght`). Le **InstanceT "Object"** est remplacé par le type de la superclass de Object qui est... **MixedT**.
- Le type **MixedT** peut être comparé à un trou noir (Object n'a pas de superclass) et que dit le moteur de règle de Flow 
dans le cas d'une contrainte **MixedT** vers **LookupT** ? Cela revient à sortir quelque chose du trou noir, ce qui est interdit,
donc une erreur est levé !




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



