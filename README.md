# react-europe-2016

## Intro



## Keynote: The Redux journey

La conférence est ouverte par Dan Abramov, introduit par Christopher Chedeaux qui rappelle la success story
qui a conduit Dan à créer Redux en préparant un talk sur [react-hot-loader](https://github.com/gaearon/react-hot-loader)
pour la précédente édition de React Europe.

Aujourd'hui chez Facebook, Dan annonce le _de facto_ premier anniversaire de Redux et revient sur son succès (3 millions
de téléchargement sur NPM, [Twitter Mobile](https://mobile.twitter.com/home) qui l'utilise) et les raisons qui ont amené
Redux à devenir l'implémentation Flux de référence.

On pense souvent que l'utilité et la qualité d'une librairie se résume à ses fonctionnalités et son API, mais dans le cas
de Redux, il s'agit d'autre chose car il n'y a basiquement pas de **fonctionnalités**, Redux se résume à un simple _change
handler_ réagissant à un événement unique et renvoyant une valeur (le state). L'intérêt de Redux est ailleurs: dans les
contraintes et les contrats d'interface qu'il impose.

Ce sont les contraintes de Redux qui font sa force, notamment en imposant un process de debug classique, et en permettant
facilement la sauvegarde / restauration de l'état (rendu coté serveur, enregistrement de la session utilisateur), les
_optimistic updates_, le _undo / redo_, etc.

Les "contrats" (que Dan présente comme des interfaces que les utilisateurs doivent implémenter eux-mêmes, à la différence
des APIs qui sont fournies) sont aussi le point de départ de riches fonctionnalités.
Certains sont spécifiques à l'utilisateur (reducer, selector) et d'autres sont externalisables en librairies tierces:

- Reducer & High Order Reducer ([redux-undo](https://github.com/omnidan/redux-undo),
[redux-optimistic-ui](https://github.com/mattkrick/redux-optimistic-ui),
[react-redux-form](https://github.com/davidkpiano/react-redux-form))
- Middleware ([redux-logger](https://github.com/evgenyrodionov/redux-logger),
[redux-observable](https://github.com/redux-observable/redux-observable) et
[apollo-client](https://github.com/apollostack/apollo-client) un client GraphQL "light")
- Store enhancer ([redux-batched-subscribe](https://github.com/tappleby/redux-batched-subscribe),
[redux-loop](https://github.com/raisemarketplace/redux-loop) et bien sûr
[redux-devtools-extension](https://github.com/zalmoxisus/redux-devtools-extension))

- Slides : http://gaearon.github.io/the-redux-journey/
- Vidéo : https://www.youtube.com/watch?v=uvAXVMwHJXU

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



## Building li.st for Android with Exponent and React Native



## GraphQL Future



## Building native mobile apps with GraphQL



## Conclusion



