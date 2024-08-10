# Chapitre : MIDDLEWARES


# Avantages du middleware

![](https://i.imgur.com/vnlWBJy.png)

### Qu'est-ce qu'un middleware ?

Le middleware Redux sert d'intermédiaire entre les créateurs et les réducteurs d'actions. Le middleware intercepte l'objet d'action avant qu'un réducteur ne le reçoive et lui donne la fonctionnalité nécessaire pour effectuer des actions supplémentaires ou des améliorations par rapport à l'action envoyée.

# Avantages du middleware

### Pourquoi l'utiliser ?

Le modèle action/réducteur est très propre pour mettre à jour l'état au sein d'une application. Mais que se passe-t-il si nous devons communiquer avec une API externe ? Ou si nous voulons enregistrer toutes les actions qui sont envoyées ? Nous avons besoin d'un moyen d'exécuter des effets secondaires sans perturber notre flux d'action/réducteur.

Le middleware permet d'exécuter des effets secondaires sans bloquer les mises à jour d'état.

Nous pouvons exécuter des effets secondaires (comme des requêtes API) en réponse à une action spécifique ou en réponse à chaque action envoyée (comme la journalisation). Il peut y avoir de nombreux middlewares par lesquels passe une action avant de se terminer dans un réducteur.

![](https://i.imgur.com/tuGKRRi.gif)

# Avantages du middleware

La syntaxe du middleware Redux est une bouchée de pain : une fonction middleware est une fonction qui renvoie une fonction et qui renvoie une fonction.

La première fonction prend le `store`comme paramètre, la deuxième prend une `next`fonction comme paramètre et la troisième prend le `action`dispatched comme paramètre.
Les paramètres `store`et `action`sont le magasin Redux actuel et l'action en cours de dispatch. La vraie magie se trouve dans la `next()`fonction.
La `next()`fonction est ce que vous appelez pour dire "ce middleware a fini de s'exécuter, passez cette action au middleware suivant". En d'autres termes, le middleware peut être asynchrone.

```
const reduxMiddleware = store => next => action => {

 . . . . . .

next(action);
};
```

# Action de journalisation

![](https://i.imgur.com/CJiWKA8.png)

Journalisation : l'un des avantages de Redux est qu'il rend les changements d'état prévisibles et transparents. Chaque fois qu'une action est envoyée, le nouvel état est calculé et enregistré. L'état ne peut pas changer de lui-même, il ne peut changer qu'en conséquence d'une action spécifique.
Ne serait-il pas agréable de consigner chaque action qui se produit dans l'application, ainsi que l'état calculé après celle-ci ? Lorsque quelque chose ne va pas, nous pouvons consulter notre journal et déterminer quelle action a corrompu l'état.

# La fonction logger :

Le middleware est appliqué dans l'étape d'initialisation de l'état avec l'enhancer applyMiddlware()

```
import { createStore, applyMiddleware  } from "redux";
```

Logger est la fonction middleware qui enregistrera l'action et l'état.

```
const logger = store => next => action => {
 console.log('dispatching', action)
 let result = next(action)
 console.log('next state', store.getState())
 return result
}
```

Il ne reste plus qu'à modifier le magasin maintenant.

```
const store = createStore(reducer, applyMiddleware(logger));
```

### Ces ressources peuvent vous aider

Intergiciels

[https://redux.js.org/advanced/middleware](https://redux.js.org/advanced/middleware)
