## Les variables

Pour déclarer une variable en javascript il suffit de mettre le mot clé `var`

```javascript
//Je déclare une variable name et je l'initialise
var name = "tony";

//et je l'affiche
console.log(name);
```

Concernant le nom de variable, il faut que celui ci doit être clair et parlant !

ex :

```javascript
var name = "tarte aux fruits"; // ❌
var cake = "tarte aux fruits"; // ✅
```

idem pour les variable composés de plusieurs mots :

```javascript
var first-name = "antho"; // ❌
/* nous pouvons voir ci dessus que le tiret n'est pas bien interpreté.
 C'est pourquoi il est interdit dans une variable. */
var prénom = "antho"; // ❌
// Ici, c'est l'accent qui pose problème.

var _firstName = "antho"; // ✅
var firstname = "antho"; // ✅
var first_name = "antho"; // ✅
var firstName = "antho"; // ✅
/* Nous allons priviliegier
le camelCase pour le nom de nos variable.*/
```

## Nous pouvons tester les types d'un élément.

Par exemple :

```javascript
var number = 123;
var bool = true;
var text = "me";
var obj = new Date();

typeof number; //'number'
typeof bool; //'boolean'
typeof text; //'string'
typeof obj; //'object'
```

Il existe aussi 2 autres type

```javascript
var testUndef;
var testNull = null;

typeof testUndef; // "undefined"
typeof testNull; // "object"
```

undefined n'existe pas du tout, alors que null est définit mais n'est rien. 😅

> Mais oui c'est clair ! | Eddy Malou

## Travailler avec les chaînes de caractères

javascript nous permet de créer une chaîne de caractère avec des doubles quotes `"[...]"` ou des single quote `'[...]'`.

Cependant, il y a des inconvénient avec les singles quotes.

```javascript

var example = 'C'est presque fini; // ❌
// Nous pouvons voir que pour JS il y a qu'un caractère, le C

var example = "C'est presque fini"; // ✅
// Ici tout rentre dans l'ordre
```

Mais il y a aussi des cas particulier avec les double quotes

```javascript

var example = "Il a dit : "C est presque fini". "; // ❌
/*
Le problème ici, c'est que nous avons ouvert avec une double quote
mais on l'a refermé juste après les :
donc JS interprete ça comme une fin alors que ça fait partie de la phrase.
💡 : pour que ce soit plus jolie, j'ai du enlever le single quote.
*/

// Ici tout rentre dans l'ordre car on à "echapper" le caractère avec un backslash.
console.log("Il à dit : \" C\'est presque fini\". "); // ✅
```

## Aborder les opérateurs

ex :

```javascript
var a = 5,
	b = 2,
	result;

result = a + b;

console.log(result);
```

Selon vous, la variable `result` est égale à combien et pourquoi ?

<details>
    <summary>Réponse</summary>
    
Le résultat = 7.

Car on assigne le résultat de l'opération mathématique à la variable `result`

</details>

---

Autre ex :

```javascript
var a = 5,
	b = 2,
	c = 2;
result;

result = a + b * c;

console.log(result);
```

Selon vous, la variable `result` est égale à combien et pourquoi ?

<details>
    <summary>Réponse</summary>
    
Le résultat = 9.

Car JS connait l'ordre de priorité de calcul donc il a fait le calcul suivant `a + (b * c)`

</details>

## Additioner et concaténer

L'opérateur `+` ne sert pas forcément à additionner 2 nombres entre eux.
Il sert aussi de signe pour concaténer 2 éléments entre eux.

ex :

```javascript
var a = 5,
	b = "2",
	result;

result = a + b;

console.log(result); // '52'
```

Si vous souhaitez que l'opérateur `+` soit l'opérateur d'addition alors vous devez être sur que les varibles soit des nombres.

```javascript
var prenom = "Antho",
	nom = "Gorski",
	result;

result = prenom + " " + nom;

console.log(result); // 'Antho Gorski'
```

Derniere choses avec les nombres

```javascript
var a = 5,
	b = "quatre",
	result;
var aNum = Number(a),
	bNum = Number(b);

result = aNum + bNum;

console.log(result); // NaN = Not a Number
/*
 En soit, ça veut nous dire que nous essayons de faire un calcul
 avec un élément qui n'est pas un number (bNum n'est pas un nombre)
*/
```

## Les templates strings

En ES6 nous avons une nouvelle façon pour concaténer une chaîne de caractère. c'est les backticks ` `` `

grâce à ça

```javascript
var firstName = "antho",
	lastName = "gorski";

// on passe de ça :
console.log(
	"Je m'appel " + firstName + " et mon nom de famille est " + lastname + "."
);

// à ça :
console.log(`Je m'appel ${firstName} et mon nom de famille est ${lastName}.`);
```

## Incrémenter et décrémenté des nombres

```javascript
var a = 2;

a = a + 10;

console.log(a); // 12
```

<details>
    <summary>Pourquoi ?</summary>
    
Car lors de l'addition, JS a fait le calcul, puis il a assigné le calcul
à la variable `a`. Il a donc écrasé l'ancienne valeur pour assigner la nouvelle valeur.
Dans se type de cas, nous pouvons l'écrire differement. 
Cette notation est plus adapté.

```javascript
var a = 2;

a += 10;

console.log(a); // 12
```

👨‍🏫 Subtilité : Quand nous devons incrémenter de 1.
(c'est à dire que le nombre augmente de 1) Il existe un raccourcie top.

```javascript
var a = 2;

a++;

console.log(a); // 3
```

</details>

## Les '6 falsy values'

Chaque élément avec une donnée, si on les convertie en boolean retournera `true`.

```javascript
var base = 2;
var bool = Boolean(base);

console.log(bool); // true
```

```javascript
var base = "Hello world!";
var bool = Boolean(base);

console.log(bool); // true
```

Sauf les six suivantes :

```javascript
var base = "";
var bool = Boolean(base);

console.log(bool); // false
```

```javascript
var base = 0;
var bool = Boolean(base);

console.log(bool); // false
```

```javascript
var base = undefined;
var bool = Boolean(base);

console.log(bool); // false
```

```javascript
var base = NaN;
var bool = Boolean(base);

console.log(bool); // false
```

```javascript
var base = null;
var bool = Boolean(base);

console.log(bool); // false
```

```javascript
var base = false;
var bool = Boolean(base);

console.log(bool); // false
```

## Allons à la rencontre des tableaux!

Grâce aux tableaux, nous pouvons faire l'accumulation de plusieurs type SANS problème !

```javascript

var testArray = [123, "Ceci est un test", true, 24];

typeof testArray; // "object"

> testArray;
< [123, "Ceci est un test", true, 24]
```

Pour accèder une donnée dans un tableau, il faut indiquer son indice.

```javascript
// exemple
> testArray[2];
< true;
```

> Mais Antho, je comprend pas, pourquoi l'indice 2 te donne 'true' alors que normalement c'est "Ceci est un test" ?

<details>
    <summary>Réponse</summary>

Tout simplement parce que dans un tableau, l'indice commence par <b>0</b>

</details>

## Travailler avec les objets

```javascript
var person = new Object();

console.log(person); // Object { }
```

À l'instar des crochet pour les tableaux, les accolades sont lié aux objets.

```javascript
var person = new Object();

person.fistName = "antho";
person.lastName = "gorski";
person.age = 28;
person.sex = "m";

console.log(person);
/*
{
    age: 28
    firstName: "antho"
    lastName: "gorski"
    sex: "m"
}
*/
```

Contrairement aux array, les objets utilisent une notation de pair. `cle: valeur`

```javascript
var person = {
	fistName: "antho",
	lastName: "gorski",
	age: 28,
	sex: "m",
};

console.log(person);
/*
{
    age: 28
    firstName: "antho"
    lastName: "gorski"
    sex: "m"
}
*/

console.log(person.firstName); // "antho"
console.log(person["age"]); // 28
```

# Sondage !

---

Pour stocker des données, les objets utilisent **\_**.

-   des méthodes
-   des paires clé-valeur
-   des containers
-   des variables

<details>
  <summary>Réponse</summary>
des paires clé-valeur
</details>

---

Un array est signalé par **\_**.

-   ()
-   []
-   //
-   {}

<details>
  <summary>Réponse</summary>
[]
</details>

---

La valeur **\_** est considérée comme valant false.

-   "false"
-   -1
-   1
-   NaN

<details>
  <summary>Réponse</summary>
NaN
</details>

---

Pour incrémenter la valeur d'une variable, on peut utiliser l'opérateur **\_**.

-   +~
-   ++
-   \*\*
-   =+

<details>
  <summary>Réponse</summary>
++
</details>

---

Pour interpoler des variables dans un template string, on utilise la syntaxe **\_**.

-   \$()
-   #()
-   \${}
-   #{}

<details>
  <summary>Réponse</summary>
${}
</details>

---

Quand une variable ne contient pas un nombre, une opération arithmétique retourne **\_**.

-   NaN
-   nil
-   #ERROR
-   undefined

<details>
  <summary>Réponse</summary>
Nan
</details>

---

L'opérateur d'assignation est **\_**.

-   =
-   =:
-   ==
-   :=

<details>
  <summary>Réponse</summary>
=
</details>

---

Le caractère d'échappement dans une chaîne est **\_**.

-   @
-   \#
-   ?
-   \

<details>
  <summary>Réponse</summary>
\
</details>

---

L'opérateur **\_** permet de connaître le type d'une variable.

-   type()
-   typeof()
-   cast()
-   datatype()

<details>
  <summary>Réponse</summary>
typeof()
</details>

---

Un nom de variable peut **\_**.

-   contenir un trait d'union
-   contenir un espace
-   contenir un souligné
-   commencer par un chiffre

<details>
  <summary>Réponse</summary>
contenir un souligné
</details>

---

Une variable non initialisée est marquée **\_**.

-   nil
-   undefined
-   empty
-   null

<details>
  <summary>Réponse</summary>
undefined
</details>
