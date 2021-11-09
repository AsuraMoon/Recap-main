# Démarrer avec React

## Découvrir la syntaxe React

Nous allons importer React sur du HTML de base grâce à [UNPCK](https://www.unpkg.com/), nous allons simplement les ajouter dans une balise `<script></script>`.

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<title>La syntaxe React</title>
		<script src="https://unpkg.com/react@16.7.0/umd/react.production.min.js"></script>
		<script src="https://unpkg.com/react-dom@16.7.0/umd/react-dom.production.min.js"></script>
	</head>
	<body>
		<div id="root"></div>

		<script>
			ReactDOM.render(
				React.createElement("h1", null, "Bonjour de React"),
				document.getElementById("root")
			);
		</script>
	</body>
</html>
```

Décrivons le script !

```javascript
ReactDOM.render(
	React.createElement("h1", null, "Bonjour de React"),
	document.getElementById("root")
);

// ReactDOM est un objet importé depuis le script
// https://unpkg.com/react-dom@16.7.0/umd/react-dom.production.min.js
/*
    Cet objet permet de rendre un contenu (c'est une méthode de ReactDOM)
    Il a besoin de 2 choses pour fonctionner :
    
    1. L'élément qu'on désire créer
        React.createElement("h1", null, "Bonjour de Réact"),
        React est importé depuis le 1er script.
           1er argument: l'élément qu'on souhaite créer.
           2eme argument: Les propriétés que je donne
           3eme argument: Les enfants de l'élément que je créer.
    2. Il faut dire ou l'on souhaite injecter cette donnée.
*/
```

## Comprendre JSX

Créer des éléments comme ci dessus c'est top, il y a un seul élément et tout va bien, cependant, vous pensez bien que react n'utilise pas que cette syntaxe car ça poses vite ses limites !

On va donc utilisé la notion de `JSX`. `JSX` veux dire `JavaScript XML` et ça permet d'écrire notre bon vieux pote HTML !

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<title>La syntaxe React</title>
		<script src="https://unpkg.com/react@16.7.0/umd/react.production.min.js"></script>
		<script src="https://unpkg.com/react-dom@16.7.0/umd/react-dom.production.min.js"></script>
	</head>
	<body>
		<div id="root"></div>

		<script>
			ReactDOM.render(
				<h1>Bonjour de React</h1>,
				document.getElementById("root")
			);
		</script>
	</body>
</html>
```

Cependant, si on essai de voir le rendu, on voit bien que ça ne marche pas.
Pourquoi ?

Car le caractère `<` n'est pas compris nativement pas le navigateur. On va donc compiler le JSX en JS classique (qui est compris par tout les navigateurs).

On va donc le confier à quelqu'un ça ! On va pas se casser la tête à le faire nous, on va utiliser [babel](https://babeljs.io/). On va importer la version [UNPKG](https://unpkg.com/browse/babel-standalone@6.26.0/) dans notre index.html dans une balise script.

Mais ça ne marche pas encore ! 🤔🤔🤔🤔🤔

Ah oui ! 😄 Il faut informer notre script qu'on utilise babel, et pour ça, on utilise l'attribu suivant :

```javascript
<script type='text/babel'></script>
```

## Créer un composant React

Plus on avance dans un projet, plus on aimerais subdiviser notre code en plus petit morceau qu'on appel composant, et chaque composant est resposable d'une partie de l'application.

Les composants sont le coeur de react, et créer des composants c'est l'activité même des développeurs React.

Comment ce passe la création d'un composant ?

Ça se passe en plusieurs étapes.

1. La création d'une classe (et on lui donne un nom). Et un composant React doit étendre (avec le mot clé `extends`) qui fait partie de la bibliothèque React.
2. Un composant de type class doit avoir une methode qui s'appelle `render()`.
3. Cette méthode retourne forcément quelque choses.

```javascript
class Bonjour extends React.Component {
	render() {
		return (
			<div>
				<h1>Bonjour de React</h1>
			</div>
		);
	}
}

ReactDOM.render(<Bonjour />, document.getElementById("root"));
```

## Créer un composant fonctionnel

Il existe d'autre manière d'écrire des composants. On appelle ça des composants 'fonctionnels' car pour créer ces composants, on utilise plus une classe en JavaScript, mais une simple fonction ! (d'ou le nom de `composant fonctionnel`)

```javascript
const Bonjour = () => (
	<div>
		<h1>Bonjour de React</h1>
	</div>
);

ReactDOM.render(<Bonjour />, document.getElementById("root"));
```

Dans notre exemple, on envoie pas de paramètres les parenthèses sont vides. Et on appel notre fonction Bonjour.

Voyez comment le code est encore plus clair. Pour récapituler, on appel un composant fonctionnel car c'est tout simplement, une fonction.

## Utiliser le CSS avec React

Ok, possons nous un peu.

On sais :

-   Créer des composants React
    -   Avec des classe JavaScript
    -   Avec des fonctions.

Maintenant, nous allons voir comment mettre du CSS !

En vrai, c'est tout aussi simple qu'avec du HTML classique 😁 SAUF à une exception près !

Déjà, nous, nous sommes des développeur, donc on veux la console de développeur ! Et pour ce faire, on va changer notre script dans l'HTML

```html
<!-- Avant -->
<script src="https://unpkg.com/react@16.7.0/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@16.7.0/umd/react-dom.production.min.js"></script>

<!-- Après -->
<script src="https://unpkg.com/react@16.7.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.7.0/umd/react-dom.development.js"></script>
```

J'ajoute ce petit code CSS pour voir si tout fonctionne bien avec le CSS.

```css
h1 {
	font-family: Arial, Helvetica, sans-serif;
}
#title {
	background-color: darkgreen;
}
.heading {
	color: #fff;
}
```

```javascript
const Bonjour = () => (
	<div id='title'>
		<h1 className='heading'>Bonjour de Réact</h1>
	</div>
);

ReactDOM.render(<Bonjour />, document.getElementById("root"));
```

Voyez comment j'ai appelé ma class, je l'ai appelé `className` et non `class``

Et oui, le mot clé `class` est déjà réservé pour créer une classe. Et noublions pas que malgrès que ça ressemble à du `HTML`c'est du `JSX` et donc du JavaScript !

## Utiliser les propriétés

Bon, on avance vachement bien je trouve, mais on va aller un peu plus loins dans notre `How to use React`.

On va tenter de rendre dynamique notre composant React. Et oui, ici, notre `h1` et en dur. On va donc modifier un peut notre composant.

```javascript
class Bonjour extends React.Component {
	render() {
		return (
			<div>
				<h1>{this.props.message}</h1>
			</div>
		);
	}
}

ReactDOM.render(
	<Bonjour message='Bonjour de React' />,
	document.getElementById("root")
);
```

Houla, toutes les nouveautés ! Décortiquons notre `class``

Déjà, nous avons `{}` les accolades. Ça indique que dans cette partie de notre JSX, nous allons passer des propriétés autrement dit des `props`.
Ensuite, on a `.message`, ça indique que je vais passer une `props` qui s'appel message. Et dans message, j'indique mon message sous forme de chaîne de caractère.

🤔 comment faire un composant fonctionnel ?

C'est tout aussi simple :

```javascript
const Bonjour = (props) => (
	<div>
		<h1>{props.message}</h1>
		<p>Vous apprenez la version {props.version} de React</p>
	</div>
);

ReactDOM.render(
	<Bonjour message='Bonjour de React' version={16} />,
	document.getElementById("root")
);
```

À la différence que nous indiquons dans notre fonction (dans les parenthèse) que nous avons des props et que nous souhaitons les utilisers.

Et pour allez plus loin :

```javascript
const Bonjour = ({ message, version }) => (
	<div>
		<h1>{message}</h1>
		<p>Vous apprenez la version {version} de React</p>
	</div>
);

ReactDOM.render(
	<Bonjour message='Bonjour de React' version={16} />,
	document.getElementById("root")
);
```

On utilise le destructuring ! J'indique que mon composant souhaite juste `message` et `version`.

## Utiliser les états

Un autre point fondamental avec react se sont les états les `states`.

Les états (on utilisera le termes `states` à l'avenir) on les utilises d'habitudes sur des composants de type `class`.

Dans notre composant `class Bonjour` on va créer une méthode qui est `constructor`.

Cette méthode sera automatiquement appelée par React au moment de `constuire` le composant.

Dit autrement, le consctructor sera appelé avant la méthode render. Le consctructor prend en charge des props.

La 1er chose que je vais faire, c'est de passer les props au composant de base avec `super()`
ensuite (et c'est la que ça nva se passer), je vais créer un composant d'état, donc un objet qui s'appel `this.state`. Et dans cet objet j'y met ce que je veux.

Dans mon cas, je vais y mettre mon prénom.

```javascript
class Bonjour extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			name: "Anthony",
		};
	}
	render() {
		return (
			<div>
				<h1>{this.props.message}</h1>
				<p>
					{this.state.name} vous apprenez la version{" "}
					{this.props.version} de React
				</p>
			</div>
		);
	}
}

ReactDOM.render(
	<Bonjour message='Bonjour de React' version={16} />,
	document.getElementById("root")
);
```

Ok, super on avance, mais en quoi c'est interactif ?

Faison un test :

```javascript
class Bonjour extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			name: "Anthony",
		};
		this.handleChange = this.handleChange.bind(this);
	}

	// handleChange est une fonction personnalisée
	handleChange(event) {
		this.setState({
			name: event.target.value,
		});
	}

	render() {
		return (
			<div>
				<h1>{this.props.message}</h1>
				<p>
					{this.state.name} vous apprenez la version{" "}
					{this.props.version} de React
				</p>
				<p>
					<input
						type='text'
						value={this.state.name}
						onChange={this.handleChange}
					/>{" "}
				</p>
			</div>
		);
	}
}

ReactDOM.render(
	<Bonjour message='Bonjour de React' version={16} />,
	document.getElementById("root")
);
```
