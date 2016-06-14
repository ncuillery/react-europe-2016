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

### Analogie avec GraphQL

Falcor est comparable à GraphQL dans le sens où ils répondent tous les deux au même problème et sont inscrit dans la mouvance 
"Demand driven architecture". Les avantages de l'un et de l'autre font qu'il y aura toujours un framework de
prédilection pour une architecture donnée.

L'avantage premier de Falcor, puisqu'on parle de lui, est son approche simplifiée. Il y a moins de concepts (schéma, requêtage, 
...). L'empreinte est moins forte et la mise en place sur une application existante est plus aisée. Pour illustrer ceci, Jeff
interroge directement un modèle Falcor via un simple _path_ JavaScript: `genrelists[0].titles[0].name` alors qu'en GraphQL il 
aurait d'abord fallu requêter le schéma puis effectuer la requête qui aurait ressemblée à ça: 
`{genrelists(first: 1): {titles(first: 1): {name}}}`.

Nous nous éloignons légèrement de la syntaxe JavaScript si on inclue des _ranges_ d'index et de propriétés dans les paths, 
par exemple `genrelists[0..1].titles[0]['name', 'rating']`, mais Jeff assure que nous avons là la totalité du "langage" de 
requêtage en Falcor. 

Viens ensuite le problème de la duplication de données, comment gérer les updates sur le modèle quand une entité s'y retrouve 
plusieurs fois (comme une série qui peut se retrouver dans plusieurs catégories par exemple) ? Un cas peut être 
pas si courant en dehors du contexte Netflix mais qui néanmoins l'objet d'une explication intéressante. Falcor gère les
doublons avec _JSON Graph_, une extension de JSON qui consiste à stocker les entités dans une collection avec un id 
(`titlesById` par exemple) et ensuite de référencer ces ids dans le modèle via une syntaxe qu'on ne verra pas (généré par une 
méthode utilitaire). Il est également possible de requêter directement la collection: `titlesById[456].name`.



## Building li.st for Android with Exponent and React Native



## GraphQL Future



## Building native mobile apps with GraphQL



## Conclusion



