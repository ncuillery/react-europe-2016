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

Cette année, pas de belles démmos, d'interfaces pimpantes pour Cheng Lou, le créateur de
[react-motion](https://github.com/chenglou/react-motion), le thème abordé est plus personnel: en tant que développeur JavaScript
on est amené à faire des choix en matière de librairies et frameworks. Cheng a mené une réflexion basée sur son expérience pour
comprendre ce qui le pousse à adopter tel ou tel librairie / framework et ainsi effectuer les bons choix de manière prédictive
sans laisser de place à une sorte d'"instinct du développeur".

### Modélisation

Imaginons un arbre descendant dans lequel les noeuds sont des couches d'abstraction, plus le noeud est haut dans l'arbre, plus le
niveau d'abstraction est élevé. Les feuilles de l'arbre sont des use-cases concrets, couvert par une abstraction de 1er niveau 
(le noeud parent aux feuilles). Nous développeurs, utilisons des abstractions pour produire quelque chose d'utile. Par exemple, 
React n'est pas utilisable en tant que tel, c'est une abstraction donnant du pouvoir aux développeurs pour produire quelque chose
d'utile (du markup par exemple). Les feuilles vertes sont les use-cases "utiles", c'est la représentation de notre produit, par
opposition aux feuilles blanches qui sont les use-cases fournis par l'abstraction mais qui ne nous intéresse pas pour notre 
produit.

Chose importante, chaque segment de l'arbre a forcément un coût, c'est le coût d'apprentissage de l'abstraction. Le choix d'une 
stack technique peut alors se résumer à la question: quelles abstractions choisir pour couvrir tous les besoins de notre 
application (feuilles vertes) avec un minimum de coût et en embarquant le minimum de noeud ?

### Librairie vs framework

Mieux vaut-il des librairies ou un framework ? C'est une question souvent débattue, Cheng cite le 
[principle of least power](https://en.wikipedia.org/wiki/Rule_of_least_power) qui plaide en faveur des librairies mais les 
frameworks, eux, revêtent une dimension sociale, ils sont capables de fédérer une communauté et donc de créer de l'entraide. 

Les frameworks correspondent aux noeuds situés très haut dans l'arbre, les librairies occupent les niveaux intermédiaires et les
feuilles peuvent être assimilé aux "micro-modules" qui ne font qu'une seule chose mais qui le font bien
([left-pad](https://www.npmjs.com/package/left-pad) par exemple :trollface:). On en trouve à foison sur NPM et c'est également
un problème (d'où l'intérêt des abstractions).

Le choix (micro-modules / librairies / frameworks) est important car selon l'expérience de Cheng, beaucoup de problèmes en
programmation proviennent d'un mauvais choix d'abstraction.

Un mauvais choix de niveau d'abstraction, que ce soit la création d'un projet open-source, d'un produit de startup, etc., 
entraîne une perte d'intérêt. Si le produit est trop concret (trop bas dans l'arbre), il y a le risque qu'il ne corresponde pas 
aux besoins (feuilles vertes non couvertes). A contrario, s'il est trop abstrait (trop haut dans l'arbre), il va décourager les
utilisateurs potentiels à cause du coût trop important.

Une autre conséquence d'un produit trop abstrait est l'éloignement vis à vis de ses propriétés intrinsèques. On risque de perdre 
de vue nos feuilles vertes et obtenir un produit qui ne correspond plus à l'idée de départ.




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



