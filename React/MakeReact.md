# Créer une application React

## Installer Node et Create React App

Ok, maintenant nous avons vu les bases de React pour commencer le développement d'une petite application.

Pour ce faire, nous devons installer et configurer un environement de développement et de test basé sur Node.js

Ça nous permettra de gérer React, ReactDOM, Babel, etc. Nous allons aussi "appréhender" [Webpack](https://webpack.js.org/).

Aller, on commence 🎉 !

Étapes :

1. On vérifie si on a installer Node.js, pour ce faire on fait la commande dans un terminal `node -v`
2. On vérifie aussi le package npm avec la commande `npm -v`

Nos 2 éléments sont installé ? Super, on continue ! Sinon, on se rend sur [Node.js](https://nodejs.org/en/) et on installe !

Nous allons installer en global un paquet qui s'appel `create-react-app` qui est créé et maintenu par Facebook. Et le faite de l'installer, ça va nous permettre de créer un environnement de développement complet pour notre appli' React. Donc, tous ce qu'on à vu jusqu'à présent sera gérer directement avec cette commande.

Pour l'installer on peux voir la [doc](https://create-react-app.dev/)

On peut aussi voir avec la commande suivante sur mac : `sudo npm install -g create-react-app`; pour windows, vous devez ouvrir votre terminal en mode administrateur. et faire la commande sans le sudo

## Utiliser Create React App

Super, maintenant nous allons maintant créer notre 1er dossier complet React.

Comme notre commande est en global sur notre ordinateur, nous avons juste à faire `create-react-app nom_du_dossier`. Bien sur que `nom_du_dossier` correspond avec le nom de votre application que vous souhaitez développer.

Par exemple, nous lors de ce cours, nous allons faire une todo-app. Donc nous faire :
`create-react-app to-do-app` OU `npx create-react-app to-do-app` si nous avons pas réussi à mettre en global notre package.

Un fois le dossier créer nous avons plein d'info.

Faisons un petit tour la-dedans.

On a d'abord un fichier qui s'appelle `package.json` qui a été génerer par la commande précédente.

Alors, on vois ici qu'on a la liste des défférents dépendances qui ont été téléchargé et installé.

Nous reconnaissons les dépendances:

```json
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-scripts": "3.0.0"
  },
```

Il y a react, react-dom ça on connait. Mais il y a aussi react-scripts et c'est ça qui va un petit peu automatiser la mise en place de notre application React, la compilation de notre code `JSX` en code javascript avec Babel. La mise en place d'un server avec webpack etc, tout ça va être automatisé par `react-scripts`.

Nous avons aussi des scripts qui permet de lancer certaines commande comme par exemple `start` qui permet de lancer notre application en local, `test` qui va tester avec `JEST` notre application etc.

Il y a le dossier `src`. C'est dans ce dossier `src` que tout se passe.

Et pour finir, le dossier public avec un `index.html` et le fameux `<div id='root'></div>`

Maintenant que nous avons fait le tour, on va faire du propre et puis commencer notre application `to-do-app` !

On supprime quasiment tout dans le dossier `src` à l'exception de `index.js` et dans se dossier on supprime tout sauf les 2 premières lignes.
Qui importe respectivement, React et ReactDOM 😁

## Créer le composant initial

⚠️ Ici, nous allons pas faire de l'html pur et dur, nous allons voir ensemble comment fonctionne React, donc on va effectivement faire vite fait un tour de [bootstrap](https://getbootstrap.com/) mais pas un cour à part entière.

Maintenant que notre `index.js` est propre, nous allons ensemble créer notre 1er composant.

Comme vu dans la session précédente, nous allons créer une classe, lui donner un nom et dire que c'est un `Component` avec le mot clé `extends`.

```JavaScript
// Nos 2 lignes de départ
import React from "react";
import ReactDOM from "react-dom";

// J'indique que je vais créer une classe App qui étend de React.Component
class App extends React.Component{
	// Il rend un élément
	render() {
		// Il retourne l'élément à rendre
		return (
			// Nous devons rendre 1 seul bloc, donc nous devons "emballer" notre rendu dans une div, section, span, p (ou <> </>, on appel ça un fragment)
			<section id='todo'>
				<h1 className='m-3'>Liste de tâches</h1>
				<ul className='list-group m-3'>
					<li className='list-group-item d-flex align-items-center'>
						Ranger la vaisselle
						<button className='btn btn-sm ml-auto btn-outline-success'>
							&#x2713;
						</button>
					</li>
					[...]
				</ul>
				<footer
					className='d-flex justify-content-between bg-secondary p-3'
					id='mainFooter'
				>
					<div className='btn-group'>
						<a href='#' className='btn btn-outline-dark bg-light'>
							List
						</a>
						<a href='#' className='btn btn-outline-dark bg-light'>
							Completed
						</a>
						<a href='#' className='btn btn-outline-dark bg-light'>
							Add
						</a>
					</div>
				</footer>
			</section>
		);
	}
}

// Une fois notre composant fini, nous appelons ReactDOM.render() et lui passons en 1er paramètre notre composant, ici App, et on 2nd paramètre la cible ou l'ont souhaite injecter le composant, ici document.getElementById("root").
ReactDOM.render(<App />, document.getElementById("root"));
```

Si on regarde notre rendu, on voit que Bootstrap n'est pas injecté, alors nous allons nous en occuper.

## Incorporer Bootstrap et Font Awesome

Nous allons maintenant intégrer Bootstrap dans notre projet pour avoir le rendu souhaité.

Pour ce faire, on va utiliser `npm` pour ajouter les dépendances à notre application.
Et au passage on va installer aussi `react-icons` qui va nous donné accès aux icones avec des librairie populaires comme Font Awesome, Material Design icons etc. Et chaque icone, sera représenté sous forme de composant react et donc, très facilement intégrables dans nos applications.

Alors on peut voir les [ressources](https://officialrajdeepsingh.medium.com/how-to-use-bootstrap-in-react-js-adf50165c7a1) de bootstrap avec react

Voici la commande :

```shell
$ npm install bootstrap react-icons jquery popper.js --save
```

Une fois téléchargé, nous allons voir directement le node_modules de bootstrap et voir le chemin `bootstrap/dist/css/bootstrap.min.css` qui est la feuille de style minifier de bootstrap.
Puis on peut aussi voir la [doc](https://react-icons.github.io/react-icons/) de react-icons et je vais importer les icones qui m'interesse.
c-à-d `{FaListAlt, FaCheckSquare, FaPlusSquare, FaTrash}` et je vais donc modifier mon composant en fonction de ce que je viens d'importer.

```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';
import 'bootstrap/dist/css/bootstrap.min.css';
import {FaListAlt, FaCheckSquare, FaPlusSquare, FaTrash} from 'react-icons/fa'


class App extends React.Component{
    render(){
        return(
            <section id="todo">
                <h1 className="m-3">Liste de tâches</h1>
                <ul className="list-group m-3">
                    <li className="list-group-item d-flex align-items-center">
                        Ranger la vaisselle
                        <button className="btn btn-sm ml-auto btn-outline-success">&#x2713;</button>
                    </li>
                    <li className="list-group-item d-flex align-items-center">
                        Répondre appel d'offres
                        <button className="btn btn-sm ml-auto btn-outline-success">&#x2713;</button>
                    </li>
                    <li className="list-group-item d-flex align-items-center">
                        Signer contrat
                        <button className="btn btn-sm ml-auto btn-outline-success">&#x2713;</button>
                    </li>
                    <li className="list-group-item d-flex align-items-center">
                        Ranger la salon
                        <button className="btn btn-sm ml-auto btn-outline-success">&#x2713;</button>
                    </li>
                </ul>
                <footer className="d-flex justify-content-between bg-secondary p-3" id="mainFooter">
                    <div className="btn-group">
                        <a href="#" className="btn btn-outline-dark bg-light"><FaListAlt /></a>
                        <a href="#" className="btn btn-outline-dark bg-light"><FaCheckSquare /></a>
                        <a href="#" className="btn btn-outline-dark bg-light"><FaPlusSquare /></a>
                    </div>
                    <button className="btn btn-outline-dark bg-light"><FaTrash /></button>
                </footer>
            </section>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('root'))
```

Et boom c'est 'beau' !

## Importer et exporter des modules

Pour le moment, toute notre application se retrouve dans notre `index.js` et ça fonctionne très bien, mais si on continue comme ça, ça deviedra infernal pour la maintenance ou l'ajout de nouvelle feature. L'intêret de react, c'est de créer des plus petits composents et qu'ils s'appelent les uns les autres.
Et nous allons donc faire ça !

Nous allons prendre tout notre composant et le mettre dans un dossier dédié que l'on appel `components` et on va créer un fichier qui s'appel `App.js`.

💡 BONNE PRATIQUE : On appel tout nos fichier component par le nom de ce qu'elle fait. Ici c'est mon App je l'appel donc `App`.
💡 BONNE PRATIQUE : Tout nos composants, à la déclaration commence par une MAJUSCULE c'est pour ça qu'ici j'ai `App.js` et non `app.js`. C'est une histoire de convention.

Une fois le fichier créé, on va _ctrl+c / ctrl+v_ notre composant à l'intérieur (en ayant au préalable importé React)

On se retrouve avec un index.js light !

On va avoir quand même 2 choses à régler.

1. importer notre App.js depuis le dossier components
2. exporter notre classe App qui se situe dans `./components/App.js`

Pour l'importer le module App, c'est facile on l'importe de la manière suivante : `import App from "./components/App"`

Ça ne fonctionne toujours pas car je n'ai pas exporté mon composant, il faut donc que je le fasse, pour ce faire, j'ajoute à la fin de mon fichier la ligne suivante : `export default App`

Et Hop ✈️ ça refonctionne ! C'est ouuuuf !

## Organiser ses composants

On ne va pas s'arreter en si bon chemin avec cette histoire de composant !

Maintenant qu'on à compris cette histoire de module, séparation en plusieurs composants, nous allons créer un composant que nous allons appeler `ToDoList.js` on import react, puis on réfléchie.
Dans notre `JSX` il y a une partie qui nous interesse plus que les autres concernant la todo c'est ce que contient la balise `ul` c'est donc cet élément que nous allons copier/coller dans notre `ToDoList.js` en oubliant pas de l'exporter.

Idem avec un composant qu'on appel `NavBar.js`, on copie/colle notre footer dans ce fichier.

Maintenant que nous avons créé d'autres composants, on les importes dans notre App.js et on les utilises.

## Créer le composant AddTask

On va créer un nouveau composant, on va l'appeler `AddTask.js`, si on fait ça, on oublie pas d'importer react, de créer une classe qui étend de component ou de créer un composant fonctionnel et de l'exporter.

```JavaScript
import React from 'react';

class AddTask extends React.Component{
    render(){
        return (
            <section>
                <h1 className="m-3">Nouvelle tâche</h1>
                <div className="card mx-3">
                    <form className="card-body" onSubmit={(e) => this.handleSubmit(e)}>
                        <div className="form-group">
                            <label form="taskName">Nom de la tâche</label>
                            <input type="text" className="form-control" name="taskName" id="taskName" required ref={input => this.newTask = input} />
                        </div>
                        <button type="submit" className="btn btn-primary">Créer</button>
                    </form>
                </div>
            </section>
        )
    }
};

export default AddTask;
```

🤔 Il sert à quoi ce composant ?

Comme son nom l'indique, il sert à ajouter une tâche, on voit un formulaire, un champ `input` et un `btn`.
Autrement dit, nous avons le formulaire qui va nous permettre d'ajouter de nouvelle tâches à notre liste.

🤔 À quel moment ce composant doit il être affiché à l'écran ?

Quand nous allons appuyer sur le 3eme bouton de notre NavBar, puis quand je clique sur le 1er bouton, je souhaite revenir sur ma liste de tâche.

C'est à dire que nous allons devoir surveiller notre ficher App.js pour savoir quoi rendre à l'utilisateur, car ce n'est pas toujours la todo qu'il souhaite mais ajouter une tâche par exemple. Nous allons devoir surveiller la barre d'adresse du navigateur. C'est en fonction de l'adresse qu'il y aura dans cette barre d'adresse qu'on va déterminer si on doit afficher `ToDoList` ou `AddTask`. Et pour surveiller ça, j'ai besoin d'une dépendances qui s'appel `react-router`.

## Incorporer react-router

[React-router](https://reactrouter.com/web/guides/quick-start) c'est un projet qui n'est pas maintenu par Facebook, c'est un projet annexe à react mais qui est très lié, bien sûr, à React!

On l'installe !

```shell
$ npm install react-router-dom --save
```

react-router est très complet. Nous allons voir ici l'intéret global, si vous souhaitez réellement le connaître, n'hésitez pas à suivre une formation sur ce projet 😁.

Une fois la dépendance installé on va pouvoir commencer :

```Javascript
import { BrowserRouter as Router, Switch, Route} from 'react-router-dom';

class App extends React.Component{
    render(){
        return(
            <section id="todo">
                <Router>
                    <Switch>
                        <Route path="/add-task" component={AddTask} />
                        <Route path="/" component={ToDoList} />
                    </Switch>
                    <NavBar />
                </Router>
            </section>
        )
    }
};
```

Explication :

1. J'import ce qui m'interesse de react-router-dom, ici c'est les 3 éléments cités ci dessus.
2. J'englobe mes composants dans un `Router`, qui possède un `switch` qui lui même possède des `routes`
3. J'indique sur chaque route, l'url à surveiller. Si l'url correspond alors affiche moi le composant associé.

## Créer des liens de navigation

Pour générer des liens qui vont envoyer nos utilisateurs vers les routes que nous avons créé précédemment, nous allons faire encore appel à `react-router-dom` et une autre de ses composante qui est `Link`.

On va changer nos lien html `<a href="#"></a>` par `<Link></Link>`.

🤔 Quelle est la différence entre les 2 ?

```javascript
import { Link } from "react-router-dom";

const NavBar = () => (
	<footer
		className='d-flex justify-content-between bg-secondary p-3'
		id='mainFooter'
	>
		<div className='btn-group'>
			<Link to='/' className='btn btn-outline-dark bg-light'>
				<FaListAlt />
			</Link>
			<Link to='/completed' className='btn btn-outline-dark bg-light'>
				<FaCheckSquare />
			</Link>
			<Link to='/add-task' className='btn btn-outline-dark bg-light'>
				<FaPlusSquare />
			</Link>
		</div>
		<button className='btn btn-outline-dark bg-light'>
			<FaTrash />
		</button>
	</footer>
);
```

On va aussi modifier notre `App.js`. Car comme vous pouvez le voir, on a une route qui s'appel `/completed` et cette route c'est la même route que ` <Route path="/" component={ToDoList} />` à la différence près que nous allons rajouter un élements (des paramètres) sur celle ci.

```javascript
// Avant
<Route path='/' component={ToDoList} />

// Après
<Route path="/:filter?" component={ToDoList} />

```

On va regarder ce qui se passe dans notre extension `React`.

Quand je clique à droite, j'ajoute une tâche, à gauche je reviens sur ma todo et au milieu, j'arrive bien à la route `/completed` mtn voyons l'ext.

Quand je me rend sur le composant `ToDoList` avec la route `/completed` j'ai des props, et dans les props, il y en à 1 qui m'intèresse c'est `match` qui possède un élément `params` et la on retrouve `filter: "completed"`

C'est grâce à se filtre que je vais pouvoir dire si je veux qu'il m'affiche tout ou simplement les tâches accomplies. Mais ça on le fera plus tard 😁

## Finaliser l'apparence de l'application

On va finir avec la finalité de notre application.

On va créer dans le dossier `src` un dossier `css` et dedans on créer un ficher `toDo.css` et dedans, vous allez copier/coller le code ci dessous

```css
body {
	background-color: #f5f5f5;
}
#toDo {
	overflow-y: auto;
	position: relative;
	padding-bottom: 70px;
}
.dot {
	height: 10px;
	width: 10px;
	border-radius: 50%;
	display: inline-block;
}
#mainFooter {
	bottom: 0;
	position: fixed;
	width: 100%;
}
.fetching {
	position: fixed;
	top: 0;
	left: 0;
	height: 100vh;
	width: 100vw;
	background-color: rgba(0, 0, 0, 0.5);
	z-index: 1000;
	display: flex;
	color: #fff;
	font-size: 5em;
	justify-content: center;
	align-items: center;
}
.spinner {
	animation: spinner 1.5s linear infinite;
}

@keyframes spinner {
	to {
		transform: rotate(360deg);
	}
}
```

Une fois fait, on importe ça dans notre `App.js` : `import './css/toDo.css'`
