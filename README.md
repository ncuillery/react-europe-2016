# react-europe-2016

## Intro



## Keynote: The Redux journey



## Native Navigation for Every Platform



## A cartoon guide to performance in React



## React Native <3 60FPS -- Improving React Native animations



## Being Successful at Open Source



## GraphQL at Facebook



## A Deepdive Into Flow



## Debugging flux applications in production



## On the Spectrum of Abstraction



## React Redux Analytics



## Evolving the Visual Programming Environment with React



## React Native Retrospective



## The Evolution of React UI Development



## Recomposing your React application



## JavaScript, React Native and Performance



## Falcor: One Model Everywhere

Les organisateurs ont fait le pari audacieux d'inviter Jafar Husain, lead dev chez Netflix pour parler de Falcor, un concurrent
du très-facebookien GraphQL. Comme GraphQL chez Facebook, Falcor est né d'un besoin interne chez Netflix: en représentant le
modèle de Netflix (Séries, Acteurs, Episodes, etc.) sous forme de graphe, on s'aperçoit que les différentes version de Netflix
(Web / Tablette / Téléphone / TV) requièrent chacune des portions différentes du modèle, chaque version n'a pas besoin des mêmes
données. Dès lors, il est difficile de fournir un _end point_ unique (en REST en tout cas).

Le rôle de Falcor est d'exposer le modèle de donnée complet en JSON. Chaque client va alors requêter le fragment de modèle qui
l'intéresse, recevoir la réponse et la cacher.

### Différences avec GraphQL

Falcor est comparable à GraphQL dans le sens où ils répondent tous les deux au même problème et sont inscrit dans la mouvance 
"Demand driven architecture". Les avantages de l'un et de l'autre font qu'il y aura toujours un framework de
prédilection pour une architecture donnée.

La particularité principale de Falcor, puisqu'on parle de lui, est son approche simplifiée. Il y a moins de concepts (schéma,
requêtage, ...). L'empreinte est moins forte et la mise en place sur une application existante est plus aisée. Pour illustrer 
ceci, Jafar interroge directement un modèle Falcor via un simple _path_ JavaScript: `genrelists[0].titles[0].name` alors qu'en 
GraphQL il aurait d'abord fallu requêter le schéma puis effectuer la requête qui aurait ressemblé à ça: 
`{genrelists(first: 1): {titles(first: 1): {name}}}`.

Nous nous éloignons légèrement de la syntaxe JavaScript si on inclut des _ranges_ d'index et de propriétés dans les paths, 
par exemple `genrelists[0..1].titles[0]['name', 'rating']`, mais Jafar assure que nous avons là la totalité du "langage" de 
requêtage en Falcor. 

Viens ensuite le problème de la duplication de données, comment gérer les updates sur le modèle quand une entité s'y retrouve 
plusieurs fois (comme une série qui peut se retrouver dans plusieurs catégories par exemple) ? Un cas peut être 
pas si courant en dehors du contexte Netflix mais qui néanmoins l'objet d'une explication intéressante. Falcor gère les
doublons avec _JSON Graph_, une extension de JSON qui consiste à stocker les entités dans une collection avec un id 
(`titlesById` par exemple) et ensuite de référencer ces ids dans le modèle via une syntaxe qu'on ne verra pas (généré par une 
méthode utilitaire). Il est également possible de requêter directement la collection: `titlesById[456].name`.

La démonstration se poursuit en se déplaçant coté serveur. Jafar explique que ce fichier JSON unique n'est qu'une vue de l'esprit 
(comment ça l'intégralité du catalogue Netflix n'est pas chargé en mémoire ?). En réalité, les requêtes Falcor sont 
interceptées et selon leur forme, le serveur va récupérer les données. Le modèle en dur utilisé jusqu'à maintenant est 
remplacé par un middleware express de routage [falcor-router](https://www.npmjs.com/package/falcor-router). Ce routeur ne 
matche non pas des urls mais les paths JavaScript.

Coté client, on a donc l'illusion d'interroger un énorme modèle JSON, alors qu'en réalité il est généré à la demande coté serveur.

### GraphQL ou Falcor, comment choisir ?

Un premier critère de choix est la dépendance vis à vis d'un schéma. Le schéma est central dans GraphQL, ce qui a énormément
d'avantages (cohérence du modèle, introspection, tooling, ...). Avec Falcor, le schéma est optionnel. En effet le modèle de
Netflix est simple, on y dénombre une vingtaine d'entités (série, film, épisode, acteur, sous-titre, ...). En comparaison 
celui de Facebook en contient plus de 3000 !

On peut très bien commencer à utiliser Falcor sans subir l'_overhead_ de la gestion d'un schéma, ce qui permet d'avancer/itérer 
plus facilement et pourquoi pas, lorsque le besoin d'une unique source de vérité se fait sentir (le modèle gagnant en complexité),
ajouter un schéma. Cerise sur le gâteau l'implémentation du schéma est libre : comme le modèle n'est qu'un pur JSON, n'importe 
quel outil permettant de structurer du JSON fait l'affaire: [TypeScript](https://www.typescriptlang.org/) ou
[JSONSchema](http://json-schema.org/) par exemple.

Le deuxième critère de choix selon Jafar est la typologie des requêtes. Les possibilités de requêtage de GraphQL sont bien 
supérieures mais l'implémentation est plus compliquée puisque toutes ces possibilités, il faut les implémenter une par une coté
serveur. De plus, en apportant de la puissance lors du requêtage, il faut également se prémunir des opérations malencontreuses 
(tri ou filtrage coûteux par exemple) en implémentant des garde-fous, etc.

Pour résumer ce point, disons que GraphQL sera plus adapté à des requêtes fortement dynamiques saisies en partie ou totalement 
par l'utilisateur comme par exemple la [recherche avancée Github](https://github.com/search/advanced). Falcor conviendra mieux 
à des applications où les requêtes sont statiques ou plus prévisibles.

A ce sujet, comment faire pour effectuer des requêtes dynamiques avec Falcor, par exemple la recherche dans Netflix, quand on a 
que des paths JavaScript à disposition ? Tout simplement en incorporant dans le modèle JSON (qui est une vue de l'esprit 
rappelons le) une map avec toutes les recherches possibles de l'utilisateur:

```javascript
{
  "a": [$ref('titlesById[23]'), ...],
  "aa": [$ref('titlesById[55]'), ...],
  // ...
  "Lady": [$ref('titlesById[55]'), ...],
  "Lady and": [$ref('titlesById[71]'), ...],
}
```

Ce principe peut être généralisé: si la requête peut être généré avec une fonction pure à N arguments, le modèle va alors contenir 
N maps imbriquées. Par exemple, si une requête à 3 parties dynamiques, le modèle aura conceptuellement une map de maps de maps avec 
toutes les valeurs possibles !

### Mon avis

Je me méfie toujours des comparatifs entre technos, mais ici Jafar ne tombe jamais dans le piège du troll et son analyse est
argumentée (à défaut d'être objective). Le talk est extrêmement bien rodé (démo vidéo timeboxée avec le temps de parole) et le 
discours fait mouche. Au final, la simplicité, les cas d'usage, la mise en place graduelle sont autant de raisons qui m'ont donné
envie de tester Falcor.



## Building li.st for Android with Exponent and React Native



## GraphQL Future



## Building native mobile apps with GraphQL



## Conclusion



