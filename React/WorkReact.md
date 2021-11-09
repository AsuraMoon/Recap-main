# Travailler avec les données dynamiques

## Travailler avec les propriétés

Ok, on à fait plein de choses dans le cours précédent mais pas encore jongler avec les données !

Nous allons donc le faire maintenant.

Petit rappel, React nous met à disposition des props et un state pour manipuler nos composants. Nous allons donc utiliser cette fonctionnalité pour notre composant `ToDoList.js`

On va commencer à parler des props.

Voilà un exemple de data que nous allons utiliser.

```JavaScript
let initialData = [
    {id: 'jsertu7a', name: 'Ranger la vaisselle', completed: false},
    {id: 'jseruo7l', name: 'Répondre appel d\'offres', completed: false},
    {id: 'jseruy2q', name: 'Signer contrat', completed: false},
    {id: 'jserv4sw', name: 'Aspirer le salon', completed: false}
]

export default initialData;
```

Détail :

Nous avons un array (tableau) qui possède 4 objets.
Les objets sont composées :

-   d'`id` unique !
-   d'un `name` qui est un string
-   d'un `completed` qui est un boolean

---

Ok, maintenant que nous avons détaillé nos données nous allons les utiliser.

Voyons le chemin: Le composant `ToDoList.js` est utilisé dans notre `App.js` et dans notre `App.js` on utilise `react-router-dom`et lui, si on regarde, on vois qu'il nous donne plein de propriétés que nous devons manipuler.

Donc pour injecter mes informations à moi je vais changer la ligne qui concerne la route `ToDoList.js` pour qu'il n'appel pas directement mon component.

Je vais faire appel à un autre élément, qui est `render` avec du code `JSX` pour signifier que je vais manipuler des éléments dedans.

```javascript
// Avant
<Route path="/:filter?" component={ToDoList} />

// Après
<Route
	path='/:filter?'
	render={(props) => <ToDoList {...props} tasks={initialData} />}
/>

/*
    Détail :
    Nous sommes encore dans notre route avec comme chemin /:filter?
    Ensuite, je ne passe plus directement par component mais par render qui me permet d'injecter de nouvelles choses.

    ici, j'indique que je vais rendre les props reçu par `react-router-dom` dans mon composant
    <ToDoList />
    Grâce au spread operator {...props} j'indique que je passe tout les props à mon composant
    Mais je peux ajouter le mien qui est `tasks` avec mes données à moi ici, initialData
*/
```

N'oublions pas que si je veux passer des props avec des données je dois importer les données.

## Afficher des données dynamiques

Maintenant que les données contenu dans notre nouveau fichier `initialData.js` sont disponible dans notre composant `ToDoList.js` nous pouvons donc les manipulers.

On va récuperer le props en mode 'descrtucturation'.
Ensuite, pour faire plus propre encore, on va créer un nouveau composant qui s'appel `ToDo.js` nous allons créer une class ToDo et dedans nous allons récuperer un `li` qui va nous servir de modèle.

Une fois fais, on retourne sur `ToDoList.js` et on va voir comment boucler sur notre tableau `tasks`.

On va manipuler des éléments donc dans notre `ul` on va ouvrir des accolades pour avertir qu'on va injecter du code.

En JavaScript, on a une méthode trop stylé qui est `map`. [map](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/map) n'est disponible que pour des tableaux (c'est pour ça que notre initialData est un tableau). Et l'intéret de map c'est qu'il execute une fonction pour chaque élément qui se trouve dans mon array.

Nous en avons 4, je vais donc éxécuter ma fonction 4 fois.

```JavaScript
import React from 'react'
import ToDo from './ToDo'

const ToDoList = ({tasks}) => (
    <>
        <h1 className="m-3">Liste de tâches</h1>
        <ul className="list-group m-3">
            {
                tasks.map((task) => <ToDo task={task} key={task.id} />)
            }
        </ul>
    </>
)

export default ToDoList
```

## Afficher des informations de manière conditionnelle

On va s'intéresser aux tâches terminée, on à 2 boutons dans notre footer, 1 bouton pour avoir toutes les tâches et 1 pour avoir les tâches terminées.

Pour ce faire, on va devoir utiliser la propriété `match` qui est injécté par `react-router-dom`. Dans cette éléments j'ai une propriété params et si je regarde, j'ai soit `undefined` si j'affiche tout soit `completed` si je clique sue le bouton complété.

Je vais devoir modifier un peu mon composant `ToDoList`, je vais utiliser ce fameux `match` et donc l'importer dans mon composant en mode desctructuring `const ToDoList = ({tasks, match})`.

Un peu de logique 🧠

Je souhaite, `si` je clique sur mon bouton qui m'affiche toutes les tâches, que ça m'affiche toutes les tâches. `sinon` j'affiche que mes task completed.

Je créer une variable `let filteredTask;` cette variable va me permettre de comparer la donnée `match`.

Je vais faire un `switch` pour que ce soit plus siimple.

```javascript
switch (match.params.filter) {
    case 'completed'
        filteredTask = tasks.filter(task => task.completed)
        break;
    default;
        filteredTask = tasks
}
```

Une fois ça fait, je peux faire un return du résultat obtenu

```JavaScript
if(filteredTasks.length === 0){
    return (
        <>
            <h1 className="m-3">Liste de tâches</h1>
            <ul className="list-group m-3">
                <li className="list-group-item">Aucune tâche à afficher</li>
            </ul>
        </>
    )
} else {
    return (
        <>
            <h1 className="m-3">Liste de tâches</h1>
            <ul className="list-group m-3">
                {
                    filteredTasks.map((task) => <ToDo task={task} key={task.id} />)
                }
            </ul>
        </>
    )
}
```

Et voilà 🥰

## Travailler avec le state

Nous affichons maintenant des données dynamiquement ! On va maintenant créer un peu d'intéractivité.

Pour ça, nous allons utiliser le `state` dans notre `ToDo`

```JavaScript
state = {
    completed: this.props.task.completed
}
```

Ici, d'indique l'état iniale de mon state, qui est par défaut l'élément reçu dans les propriétés.

Mais pour modifier le `state` nous devons le spécifier dans une fonction que nous allons appeler `toggleClompleted`

```JavaScript
toggleCompleted = () => {
    // ici prevState est l'ancienne version de notre state
    this.setState(prevState => ({
        // Nous indiquons que completed vaut l'inverse de notre ancien state
        completed: !prevState.completed
        // Si prevState.completed vaut true, completed vaudra false
        // Si prevState.completed vaut false, completed vaudra true
    }))
}
```

Et pour utiliser cette fonction nous sommes obligé d'informer notre bouton qui indique si oui ou non le bouton est `cliqué`

```JavaScript
<button
    className="btn btn-sm ml-auto btn-outline-success"
    onClick={() => this.toggleCompleted()}>&#x2713;
</button>
```

🤔 Pourquoi faire une fonction dans mon `onClick` ?

Car nous avons besoins d'avoir le retour de notre notre fonction.
C'est à dire d'avoir le retour de notre nouveau state.

🚨 même si ça peut fonctionner sans indiquer qu'il s'agit d'une fonction dans notre onClick, il est recommandé de le faire quand même.

Ensuite, on va faire un peut de CSS conditionnelle

```javascript
return (
	<li
		className={
			"list-group-item d-flex align-tiems-center " +
			(this.state.completed ? "bg-success" : null)
		}
	>
		{this.props.task.name}
		<button
			className={
				"btn btn-sm ml-auto " +
				(this.state.completed ? "btn-success" : "btn-outline-success")
			}
			onClick={() => this.toggleCompleted()}
		>
			&#x2713;
		</button>
	</li>
);
```

## Passer des fonctions en priorités

Maintenant que visuellement ça marche, est ce que ça fonctionne dans notre application ?
Cliquons sur une tâche, maintenant allons voir si celles-ci est vraiment completé.

Et bien non, et si on reviens sur la liste de toutes les tâches, celle que nous avons selectionné elle ne l'est plus. Nous devons donc rendre l'élément persistant.

Pour ce faire, nous allons aller dans notre `App` pour le modifier un peu.

Dans celui ci, nous allons lui ajouter aussi un objet state avec comme élément

```JavaScript
state = {
    tasks: initialData
}
```

Du coup on change aussi un peu notre .map

```JavaScript
// Avant
<Route path="/:filter?" render={(props) => <ToDoList {...props} tasks={initialData} />} />

// Après
<Route path="/:filter?" render={(props) => <ToDoList {...props} tasks={this.state.tasks}/>} />
```

On peut voir ce que ça donne, on vois grâce à notre application que maintenant je reçois bien les informations de mon state.

On va créer une fonction qui va changer notre state, pour ça on va l'appeler `onToggleChange`
Cette fonction va recevoir un argument, cette argument est l'id de la tâche qu'on souhaite marquer comme faite, on va l'appeler `taskId`.

🤔 Elle va faire quoi cette fonction ?

Cette fonction va créer une variable, qu'on appelera `taskToUpdate` et cette variable, sera égale à notre tasks de notre state donc `this.state.tasks` on va lui ajouter la méthode `find()` car je vais aller rechercher la liste des tâches à modifier. Et celles que je souhaite modifier c'est `task => task.id === taskId` celle qui est passé en paramètre.

Maintenant que j'ai trouvé la tâche que je dois modifier, je vais réellement la modifier. donc `taskToUpdate.completed = !taskToUpdate.completed`. Donc maintenant, si `taskToUpdate` vaut false ça passe à true, et si c'est true, ça passe à false !

Youhou !!!!

Maintenant que j'y arrive, je vais le dire à mon state avec `setState`.

Le code final vaut

```JavaScript
// App.js

state = {
    tasks: initialData
}

onToggleCompleted = (taskId) => {
    let taskToUpdate = this.state.tasks.find(task => task.id === taskId)
    taskToUpdate.completed = !taskToUpdate.completed

    // Je récupère le state précédent avant changement
    this.setState(prevState => (
        // Je boucle dessus avec un .map car c'est un array et je souhaite
        // Executer une fonction
        prevState.tasks.map(task => {
            // J'indique que je retourne task.id avec une opération ternaire
            return task.id === taskId ?  taskToUpdate : task

            // Si task.id === taskID alors, je retourne le changement
            // Sinon je retourne ma tâche tel quelle.
        })
    ))
}
```

Bon, bon, bon, on a un problème.. Parce que ma fontion `onToggleCompleted` se trouve dans mon `App` alors que mon bouton lui se trouve dans `ToDo.js`. Et bien c'est très simple, on va le passer sur forme de props ! Comment ? Je l'ajoute dans mon composant ToDoList

```JavaScript
// App.js
<Route path="/:filter?" render={(props) => <ToDoList {...props} tasks={this.state.tasks} onToggleCompleted={this.onToggleCompleted} />} />

```

Ensuite je vais dans mon composant `ToDoList.js` et je le récupère en desctructuring

Voilà le code dans mon composant `ToDoList` j'ajoute la fonction `onToggleCompleted` et tant que props dans mon composant `ToDo`

```JavaScript
// ToDoList.js
return (
    <>
        <h1 className="m-3">Liste de tâches</h1>
        <ul className="list-group m-3">
            {
                filteredTasks.map((task) => <ToDo task={task} key={task.id} onToggleCompleted={onToggleCompleted} />)
            }
        </ul>
    </>
)
```

Pour finir avec ma ToDo

```JavaScript
// ToDo.js
toggleCompleted = () => {
    this.setState(prevState => ({
        completed: !prevState.completed
    }))
    this.props.onToggleCompleted(this.props.task.id)
}
```
