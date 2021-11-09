# Mettre en place les bases

## Aborder les prérequis

React est une bibliothèque JavaScript qui est utilisée pour créer des interfaces utilisateur développés par Facebook !

En 2011, Facebook commence, puis en 2012 c'est Instagram qui s'y met !

En 2013, Facebook décide d'open sourcer Reactjs et une importante communauté de développeurs s'est formée autour de cette bibliothèque.

On va (re)partir de 0 avec React !
Et vu que React c'est du JS donc on part du principe que c'est good avec ça (HTML/CSS aussi)

## Découvrir React

Avant toute chose, nous devons connaître le principe général de react. React a la réputation d'être très léger et très rapide.

ET C'EST VRAI !

Pour pallier aux performance de manipulation du DOM. React va en créer un virtuellement (un DOM virtuel). Ce virtual DOM est parfaitement synchrone avec le DOM réel. Alors, qu'elle est la différence ? La différence c'est que ce virtual DOM est un objet javascript (Encoooore, ça fait beaucoup la non ?) résident en mémoire et donc l'accès à cet objet est quasiment instantané.

En gros, quand on dis de faire une modification ou lire une data, au lieu de lire dans le vrai DOM trop de ressource React va lire les informations dans le DOM virtuel. Et une fois ce changement fait, celui ci va comparer avec le DOM physique et si il y a un changement il va écrire ces changements dans le vrai DOM mais de manière opti' !

C'est compliqué hein ?

Rassurez vous, react s'occupe de tout ! En tant que dev' vous n'allez pas directement manipuler ni le DOM du navigateur, ni le virtual DOM ! On utilisera l'API de React.

## Outils

On va installer l'ext REACT pour voir si notre site est sous REACT ou pas :)

## Utiliser ES6

Petit tour de l'ES6 !

### Les fonctions

```javascript
// Avant
function add() {
	return 2 + 4;
}

// Après
const add = () => {
	return 2 + 4;
};
```

### Le spread operator

```javascript
// Avant

const colors = ["red", "green", "blue"];
const newColor = colors.concat("yellow");

// Après
const colors = ["red", "green", "blue"];
const newColor = [...colors, "yellow"];
```

Les `...` est l'annotation du spread operator, voyons la [doc](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Op%C3%A9rateurs/Syntaxe_d%C3%A9composition)

### Destructuration des objets

```javascript
// Avant
var person = {
	fName: "Anthony",
	lName: "Gorski",
};

function logName(person) {
	console.log(`Vous vous appelez ${person.fName} ${person.lName}`);
}

// Après
function logName({ fName, lName }) {
	console.log(`Vous vous appelez ${fName} ${lName}`);
}

logName(person);
```
