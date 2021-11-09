# Utiliser la syntaxe conditionnelle

Admettons que la condition suivante.

```javascript
// Age est un nombre (pas de quote)
var age = 25;

/*
Une bonne question en javascript c'est une question qui peut se répondre
soit par 'true' soit par 'false'

Si c'est autre chose, alors la question est mauvaise !
*/

// SI age est superieur ou égal à 18 alors
if (age >= 18) {
	// Fait ce bloc d'instruction
	console.log(`À ${age} ans, vous êtes majeur.`);
}
// Sinon
else {
	// Fait ce code la
	console.log(`À ${age} ans, vous êtes encore mineurs`);
}
```

Selon vous, la console va afficher quel réponse si age = 25 ?

<details>
    <summary>Réponse</summary>
    Si age = 25; Alors la réponse au if = true (25 > 18)
    Donc on execute le console.log du if !

```html
À 25 ans vous êtes majeur.
```

</details>

## Opérateur ternaire

L'opérateur ternaire est une variante du IF simple.

```javascript
// Age est un nombre (pas de quote)
var age = 25;

// syntaxe
// question ? valeur vrai : valeur faux;

// Question
age >= 18
	? // valeur vrai
	  console.log(`À ${age} ans, vous êtes majeur.`)
	: // valeur faux
	  console.log(`À ${age} ans, vous êtes encore mineurs`);
```

C'est une façon de faire que vous allez rencontrer beaucoup de fois en JS.

## Les opérateurs de comparaison

```javascript
var a = 2;
var b = 1;

// Si a est égal à b alors
if (a == b) {
	// Fait ce bloc d'instruction
	console.log("La réponse est true");
}
// Sinon
else {
	// Fait ce code la
	console.log("La réponse est false");
}
```

Opérateur d'égalité :

-   `==`
    -   Celui ci compare si le nombre à gauche est le même qu'à droite
-   `===`
    -   Ceci est la strict égalité, c'est à dire qu'il va vérifier le contenu et son type.
-   `!=`
    -   Celui ci c'est l'opérateur d'inegalité, en soit il va vérifier si l'un est différent de l'autre.
-   `!==`
    -   Celui ci c'est l'opérateur de strict d'inegalité, en soit il va vérifier si l'un est différent de l'autre ainsi que son typage.
-   `>` ou `>=`
    -   Plus grand que OU plus grand ou égal
-   `<` ou `<=`
    -   Plus petit que OU plus petit ou égal

## Découvrir les boucles

### While / Do While

Dans votre parcours de dev', vous allez avoir besoins de répéter des insctructions de code plusieurs fois.

C'est pourquoi, nous allons voir ensemble la boucle **while**

```javascript
var a = 1;

// tant que a est plus petit que 10 alors éxécute le code suivant
while (a < 10) {
	console.log(`La valeur de la variable a = ${a}`);
}
```

<details>
    <summary>Remarque</summary>

Avec le code suivant, nous allons rentrer dans une boucle infini. Et ça, c'est pas top..
Donc, pour pouvoir sortir de ce bourbier, il faut qu'on incremente la variable a de 1.

```javascript
var a = 1;

while (a < 10) {
	console.log(`La valeur de la variable a = ${a}`);
	a++;
}

console.log("Boucle fini !");

/*
La valeur de la variable a = 1
La valeur de la variable a = 2
La valeur de la variable a = 3
La valeur de la variable a = 4
La valeur de la variable a = 5
La valeur de la variable a = 6
La valeur de la variable a = 7
La valeur de la variable a = 8
La valeur de la variable a = 9
Boucle fini !
*/
```

</details>

Sont alter ego, le **do while**

```javascript
var a = 1;

do {
	console.log(`La valeur de la variable a = ${a}`);
	a++;
} while (a < 10);
```

La, vous vous demandez pourquoi faire de cette façon, c'est très simple, car dans le **do while** on éxécute le code au moins 1 fois, puis après on vérifie la condition.

```javascript
var a = 18;

do {
	console.log(`La valeur de la variable a = ${a}`);
	a++;
} while (a < 10);

/*
La valeur de la variable a = 18
*/
```

Pour êtree honnete, le do while n'est pas très utilisé.

## Boucle for

```javascript
// La boucle for permet en 1 ligne de déclarer plusieurs élément
/*
    Composition des 3 éléments qui controle la boucle
    1/ la variable de controle (i dans notre cas)
    2/ Condition à vérifier
    3/ Incrémentation de la variable
    for(1; 2; 3) {
        [...]
    }
*/
for (var i = 0; i < 10; i++) {
	console.log(`La valeur de la variable i = ${i}`);
}
```

## Mots-clés

### CONTINUE

Le mot clé `continue` permet de sortir de l'itération en cour de la boucle, mais je vais quand même continuer les itérations qu'il reste à faire.

```javascript
for (var i = 0; i < 10; i++) {
	if (i == 5) {
		continue;
	}
	console.log(`La valeur de la variable i = ${i}`);
}
```

En sachant ça, à votre avis, la console va nous afficher quoi ?

<details>
    <summary>Réponse</summary>

```javascript
/*
La valeur de la variable i = 1
La valeur de la variable i = 2
La valeur de la variable i = 3
La valeur de la variable i = 4
La valeur de la variable i = 6
La valeur de la variable i = 7
La valeur de la variable i = 8
La valeur de la variable i = 9
*/
```

</details>

### BREAK

Le mot-clé `break` quand à lui, il stop complétement sortir de la boucle.

```javascript
for (var i = 0; i < 10; i++) {
	if (i == 5) {
		break;
	}
	console.log(`La valeur de la variable i = ${i}`);
}
```

En sachant ça, à votre avis, la console va nous afficher quoi ?

<details>
    <summary>Réponse</summary>

```javascript
/*
La valeur de la variable i = 1
La valeur de la variable i = 2
La valeur de la variable i = 3
La valeur de la variable i = 4
*/
```

</details>

## Boucle foreach

La boucle **foreach** a été spécialement conçu pour boucler sur les collections<sup>\*</sup> de javascript

🔓 une collection est une variable qui contient plusieurs données, c'est à dire. Un Array ou un Objet.

en soit, une boucle foreach peut se traduire par
_Pour chaque_ [...]

```javascript
var fruits = ["banane", "kiwi", "orange"];
var animals = {
	species: "dog",
	name: "gallia",
	weight: "20kg",
	age: 8,
};

// Voici sa structure
/*
    1/ le nom d'une variable
    2/ le nom de l'array ou de l'objet autour duquel je désir boucler

    for(1 in 2) {

    }   
*/
// Nous pouvons traduire la ligne ci dessus comme suit
// POUR fruit DANS l'array fruits
for (fruit in fruits) {
	/* La variable fruit, c'est moi qui l'ai choisis
        elle correspond avec mon tableau pour une question
        de clarté
    */
	console.log(fruit);
	/* 
        0
        1
        2
    */
	console.log(`Mon fruit préféré est le ${fruits[fruit]}`);
}

for (prop in animals) {
	console.log(prop);
	/*
        species
        name
        weight
        age    
    */

	console.log(`La valeur de la clé de ${prop} est ${animals[prop]}`);
}
```

## Sondage !

Pour utiliser une boucle `for` sur les éléments d'un array, on utilise le mot-clé **\_**.

-   between
-   loop
-   each
-   in

<details>
    <summary>Réponse</summary>
in
</details>

---

Le mot-clé **\_** arrête les itérations d'une boucle.

-   exit
-   quit
-   break
-   leave

<details>
    <summary>Réponse</summary>
break
</details>

---

Dans la boucle `for`, il est obligatoire de nommer la variable `i`.

-   FAUX
-   VRAI

<details>
    <summary>Réponse</summary>
FAUX
</details>

---

Dans une boucle `while`, il faut penser à **\_** la valeur.

-   récupérer
-   définir
-   stocker
-   incrémeter

<details>
<summary>Réponse</summary>
Incrémenter
</details>

---

L'opérateur de comparaison d'égalité est **\_**.

-   ==
-   eq
-   =
-   !==

<details>
<summary>Réponse</summary>
==
</details>

---

L'opérateur ternaire commence par le symbole **\_**.

-   &
-   ?
-   :
-   \$

<details>
<summary>Réponse</summary>
?
</details>

---

La syntaxe conditionnelle commence par `if` et peut contenir un **\_**.

-   elsif
-   elseif
-   elif
-   else

<details>
<summary>Réponse</summary>
else
</details>
