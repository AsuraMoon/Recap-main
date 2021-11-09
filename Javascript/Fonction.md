# Créer des fonctions

## Engendrer des fonctions simple

Dans le javascript moderne, on peut dire que tout ou presque est `fonction`.
En anglais, on appel ça le _functionnal programming_ est cette façon est de plus en plus populaire.

Il va de soit que les scripts vont rapidement se compléxifier, il sera donc primordial de garder un code clair, propre et facile à maintenir.

Il faudra pour ça, éclater votre script en module plus petit pour lesquel vous allez leur donner des noms.

Voilà le principe des `function` en javascript. C'est à dire un bloc pour lequel vous allez donner un nom et l'appeler plusieurs fois.

Faire une fonction à partir de l'exemple ci-dessous :

```javascript
var a = 2,
	b = 5,
	result;

result = a + b;
console.log(result);
```

<details>
<summary>Réponse</summary>

Nous devons le faire en plusieurs étape:

-   Délimiter le bloc de code que ma fonction devra éxécuter
-   Nous devons lui donner un `nom`
-   Il faut ajouter le mot-clé `function`
-   Il faut aussi ajouter après le nom de la fonction une paire d'accolade (Nous allons voir ça plus tard)

```javascript
var a = 2,
	b = 5,
	result;

// résultat final
function add() {
	result = a + b;
	console.log(result);
}

/****** AUTREMENT ******/

var add = function () {
	result = a + b;
	console.log(result);
};

// Pour éxécuter la fonction, il faut l'appeler.
// donc ici nous appelons la fonction en mettant les parenthèses.
// ce sont elles qui marque le faite qu'on veux éxécuter la fonction
add();
```

Allons voir quel est le typeof de add !

</details>

## Envoyer des données dans une fonction

L'un des avantages des fonctions, c'est qu'on peut l'éxécuter plusieurs fois !

```javascript
var a = 2,
	b = 5,
	result;

function add() {
	result = a + b;
	console.log(result);
}

add();
add();
```

C'est fou ! Maintenant qu'on l'a créer, la fonction add() on peut l'utiliser un nombre ilimité de fois ! C'EST OUUUUUF !!😮 😮

Par contre, on va pas se mentir, retourner 1 seul résultat... Ça, c'est moi ouf..

C'est pourquoi les parenthèses de la fonction sont là.

```javascript
var a = 2,
	b = 5,
	result;

// num1 et num2 sont des arguments. Ils sont passé à la fonction
// pour faire l'addition de 2 nombres.

function add(num1, num2) {
	result = num1 + num2;
	console.log(result);
}

add(a, b);
add(7, 5);
```

Maintenant que nous avons fait ça, notre fonction est plus intelligente qu'avant !

#Question !

Que se passe t'il selon vous si je fait ça :

```javascript
var result;

function add(num1, num2) {
	result = num1 + num2;
	console.log(result);
}

// Question1
add(1, 8, 9);

// Question2
add(5);
```

<details>
<summary>Réponse</summary>

-   question 1
    -   Et bien rien ! Tout simplement car le 3eme argument n'est pas pris en compte dans notre function.
-   question 2
    -   Nous allons avoir 1 erreur (NaN) car on le 2eme argument est undefined donc 5 + undefined = NaN. Pour pallier à ça, nous pouvons donner une valeur par défaut.

```javascript
function add(num1 = 2, num2 = 5) {
	result = num1 + num2;
	console.log(result);
}
```

</details>

## Retourner les données d'une fonction

L'objectif d'une fonction, n'est pas de retourner un `console.log()` mais bien de retourner une valeur que je peux manipuler ailleur dans mon script.

Pour cela, nous devons changer un peu notre fonction.

```javascript
/*
Nous n'avons plus besoin du result en global,
donc nous pouvons l'enlever
*/

function add(num1 = 0, num2 = 0) {
	// et le déclarer dans la fonction add()
	var result = num1 + num2;
	// le mot-clé 'return' est la pour spécifier que nous voulons
	// retourner le résultat de l'addition.
	return result;
}

// ce resultat est stocké dans la variable addNumbers
var addNumbers = add(1, 8);

// Puis on affiche celui ci dans la console.
console.log(addNumbers);
```

## Éxecuter immédiatement des fonctions

Créer des fonctions se passe en 2 temps.

-   On la défini
-   On l'éxecute

Il existe une syntaxe qui permet de définir une fonction et de l'appeler directement après.

Il s'agit de `IIFE = Immediately Invoked Function Execution`

La syntaxe est assez simple :

```javascript
// 2 paires de parenthèses.

/*

La 1er, il s'agit de définir la fonction
la 2nd, marque l'éxécution immédiate de la fonction que j'ai défini
dans la 1er paire de parenthèse.
*/

(function () {
	var result = 2 + 4;
	console.log(result);
})();
```

<details>
<summary>Pour aller plus loin</summary>

```javascript
(function (num1, num2) {
	var result = num1 + num2;
	console.log(result);
})(5, 10);
```

</details>
Cette fonction comme vous avez pu le constater, elle n'a pas de nom. C'est normal, vu que nous l'éxécutons qu'une seul fois, et comme je n'aipas besoin de l'appeler plusieurs fois, je n'ai pas besoin de la nommé.
Nous avons ici notre 1er `fonction anonyme !`

## Appréhender les fonctions à flèche (arrow function)

ES6 est une version (relativement) moderne du javascript défini encore une syntaxe pour créer des fonctions.

OBJECTIF : rendre le code plus lisible et moins verbeux.

EX :

```javascript
((num1, num2) => {
	var result = num1 + num2;
	console.log(result);
})(5, 10);
```

⌛ Nous reviendrons en détail plus tard parce que les fonctions fléchés c'est top !

⚠️ Ce qu'il faut retenir :

Quand on voit la fleche `=>` il s'agit d'une nouvelle syntax pour définir les fonctions.

## Comprendre la portée des variables

Nous pouvons voir ici que la variable `result` se trouve en dehors de la fonction.

Et dans la fonction on voit bien que je peux manipuler cette variable `result` sans problème.

Cela veut dire que `result` est dans le _global scope_
c'est à dire disponible de partout et à tout moment.
(Visible à l'intérieur d'une fonction, mais aussi à l'éxtérieur de celle ci)

```javascript
var result;

function add(num1, num2) {
	result = num1 + num2;
	console.log(result);
}

add(1, 8);
```

expérience :

```javascript
function add(num1, num2) {
	var result;
	result = num1 + num2;
}

add(1, 8);
console.log(result); // ERROR | result is not defined
```

Quand on déclare des variables à l'intérieur d'une fonction, sa porté est limitée au corp de la fonction dans lequel elle est défini. Elle n'est plus global.

## Utiliser LET pour déclarer des variables

Nous allons changer la façon de déclarer nos variable.
C'est un nouveau mot-clé introduit par ES5 une version (relativement) récente du javascript. Nouveau mot-clé qui nous permet de gérer au mieux la porté de nos variable.

```javascript
let result;

function add(num1, num2) {
	result = num1 + num2;
	console.log(result);
}

add(1, 8);
```

Ici, le mot-clé `LET` permet de déclarer des variables dont la porté est limité dans le corp dans laquel la variables est déclare.

Dans mon cas, c'est l'ensemble de mon code (donc pas de différence avec var)

experience :

```javascript
//Experience 1
function add(num1, num2) {
	if (true) {
		var result = num1 + num2;
	}
	console.log(result);
}

add(1, 8); // 9

// Experience 2
function add(num1, num2) {
	if (true) {
		let result = num1 + num2;
	}
	console.log(result);
}

add(1, 8); // ERROR | result is not defined
```

<details>
<summary>Pourquoi l'erreur ?</summary>

Tout à l'heure j'ai dis :

> Ici, le mot-clé `LET` permet de déclarer des variables dont la porté est limité dans le corp dans laquel la variables est déclare .

Ici, la limite de notre variable est le `if()`

Pour que ça fonctionne, il faut mettre le `console.log()` à l'intérieur du `if`

```javascript
// Experience 2
function add(num1, num2) {
	if (true) {
		let result = num1 + num2;
		console.log(result);
	}
}

add(1, 8); // 9
```

</details>

## Utiliser CONST pour déclarer des variables

Idem que pour `LET`, `CONST` provient de ES5 et permet de déclarer des constantes.

Une constante est une variable qui ne changera jamais.

```javascript
const firstName;

console.log(firstName); // missing = in const declaration

```

Il faut donc

-   déclarer la variable entant que constante
-   l'initialiser au même moment

```javascript
const firstName = "antho";

console.log(firstName); // "antho"
```

experience :

```javascript
const firstName = "antho";

firstName = "patrick";

console.log(firstName); // "invalid assignment to const firstName"
```

⚠️ La convention de variable de type `const` s'écrit toujours en MAJUSCULE.

```javascript
const FIRSTNAME = "antho";

console.log(FIRSTNAME); // "antho"
```

## Sondage

L'ECMAScript 5 introduit le mot-clé **\_** pour déclarer une constante.

-   def
-   immut
-   set
-   const

<details>
<summary>Réponse</summary>
const
</details>

---

Le mot-clé **\_** permet de déclarer des variables dont la portée est limitée au bloc de code.

-   local
-   var
-   set
-   let

<details>
<summary>Réponse</summary>
let
</details>

---

Une variable définie dans une fonction est de portée globale.

-   VRAI
-   FAUX

<details>
<summary>Réponse</summary>
FAUX
</details>

---

La syntaxe ECMA6 d'invocation directe d'une fonction est **\_**.

-   \$>
-   =>
-   \>>
-   ->

<details>
<summary>Réponse</summary>
=> (fonction fléché)
</details>

---

La syntaxe `()()` définit une **\_**.

-   FICA
-   AFDE
-   IIFE
-   UDFE

<details>
<summary>Réponse</summary>
IIFE
</details>

---

Le mot-clé **\_** permet de définir la valeur de retour d'une fonction.

-   result
-   return
-   set
-   define

<details>
<summary>Réponse</summary>
return
</details>

---

Les parenthèses d'une fonction permettent de préciser des **\_**.

-   valeurs
-   opérateurs
-   objets
-   paramètres

<details>
<summary>Réponse</summary>
paramètres
</details>

---

Une fonction est **\_**.

-   un bloc de code
-   une assignation
-   une boucle
-   une variable

<details>
<summary>Réponse</summary>
un bloc de code
</details>
