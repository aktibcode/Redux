# Chapitre : REFLEXION REDUX (Redux Thunk)


# Qu'est-ce que redux-thunk ?

Thunk est un autre mot pour une fonction, mais ce n'est pas n'importe quelle fonction. C'est un nom spécial (et peu courant) pour une fonction renvoyée par une autre.

```
function wrapper_function() {
 // this one is a "thunk" because it defers work for later:
 return function thunk() {
   // it can be named, or anonymous
   console.log("do stuff now");
 };
}
```

Vous connaissez déjà ce modèle. Vous ne l'appelez simplement pas « thunk ». Si vous souhaitez exécuter la partie « faire quelque chose maintenant », vous devez l'appeler comme wrapper_function()() – en l'appelant deux fois, en gros.

# Alors, comment cela s’applique-t-il à Redux ?

Eh bien, à présent, nous savons que Redux dispose de quelques outils principaux : il existe des « actions », des « créateurs d’actions », des « réducteurs » et des « intergiciels ».
Les actions ne sont que des objets. En ce qui concerne Redux, les actions prêtes à l’emploi doivent être des objets simples et elles doivent avoir une propriété de type. En dehors de cela, elles peuvent contenir tout ce que vous voulez, tout ce dont vous avez besoin pour décrire l’action que vous souhaitez effectuer.
Les actions ressemblent à ceci :

```
// 1. plain object
// 2. has a type
// 3. whatever else you want
{
 type: "USER_LOGGED_IN",
 userName: "dave"
}
```

# Réflexion de Redux :

Comme il est assez ennuyeux d'écrire ces objets à la main tout le temps (sans parler du risque d'erreur), Redux a l'option des « créateurs d'actions » pour éliminer ces choses :

```
function userLoggedIn() {
 return {
   type: "USER_LOGGED_IN",
   username: "dave"
 };
}
```

Il s'agit exactement de la même action, mais vous pouvez désormais la « créer » en appelant la fonction userLoggedIn. Cela ajoute simplement une couche d'abstraction.

Au lieu d'écrire l'objet d'action vous-même, vous appelez la fonction, qui renvoie l'objet. Si vous devez envoyer la même action à plusieurs endroits de votre application, l'écriture de créateurs d'action facilitera votre travail.

# Réflexion de Redux :

En fait, les actions Redux ne font rien. Ce ne sont que des objets. Pour les faire réaliser une action concrète (appeler une API, déclencher une autre fonction…), nous devons nous assurer que le code réside dans une fonction. Cette fonction (également appelée thunk) est un ensemble de travail à effectuer. En ce moment, notre créateur d’action exécute une action. Comme le montre l’exemple ci-dessous

```
function getUser() {
 return function() {
   return fetch("/current_user");
 };
}
```

# Réflexion de Redux :

Si seulement il existait un moyen d’apprendre à Redux à gérer les fonctions comme des actions.

Eh bien, c'est exactement ce que fait redux-thunk : c'est un middleware qui examine chaque action qui passe par le système, et s'il s'agit d'une fonction, il appelle cette fonction. C'est tout ce qu'il fait.
La seule chose que j'ai omise de ce petit extrait de code est que Redux passera deux arguments aux fonctions thunk :
Dispatch, afin qu'elles puissent envoyer de nouvelles actions si nécessaire ;
getState, afin qu'elles puissent accéder à l'état actuel.

Voici un exemple pour l'illustrer :

```
function logOutUser() {
 return function(dispatch, getState) {
   return axios.post("/logout").then(function() {
     // pretend we declared an action creator
     // called 'userLoggedOut', and now we can dispatch it
     dispatch(userLoggedOut());
   });
 };
}
```

*la fonction getState peut être utile pour décider s'il faut récupérer de nouvelles données ou renvoyer un résultat mis en cache, en fonction de l'état actuel.*

# Réflexion de Redux :

Configurez redux-thunk dans votre projet.
Si vous avez un projet sur lequel Redux est déjà configuré, l'ajout de redux-thunk se fera en deux étapes.
Tout d'abord, **installez le paquet** .

```
npm install --save redux-thunk
```

Ensuite, où que vous ayez votre code d’installation Redux, vous devez **importer redux-thunk et insérer son middleware dans Redux :**

```
// You've probably already imported createStore from 'redux'
// You'll need to also import applyMiddleware
import { createStore, applyMiddleware } from "redux";

// Import the `thunk` middleware
import thunk from "redux-thunk";

// Import your existing root reducer here.
// Change this path to fit your setup!
import rootReducer from "./reducers/index";

// The last argument to createStore is the "store enhancer".
// Here we use applyMiddleware to create that based on
// the thunk middleware.
const store = createStore(rootReducer, applyMiddleware(thunk));
```

Assurez-vous simplement d'envelopper thunk dans l'appel applyMiddleware, sinon cela ne fonctionnera pas.
Après cela, vous êtes prêt : vous pouvez maintenant envoyer des fonctions qui font tout ce dont vous avez besoin.

### Ces ressources peuvent vous aider

redux - réfléchissez aux bases

[https://medium.com/fullstack-academy/thunks-in-redux-the-basics-85e538a3fe60](https://medium.com/fullstack-academy/thunks-in-redux-the-basics-85e538a3fe60)

réflexion redux

[https://github.com/reduxjs/redux-thunk](https://github.com/reduxjs/redux-thunk)
