# Chapitre : REDUX AVEC HOOKS


# Redux avec des crochets

Lorsque React a publié la mise à jour Hooks, Redux l'a suivie en proposant un ensemble d'API hook comme alternative au composant d'ordre supérieur connect() existant. Ces API vous permettent de vous abonner à la boutique Redux et d'envoyer des actions sans avoir à encapsuler vos composants dans connect().
Ces hooks ont été ajoutés pour la première fois dans la version 7.1.0.

![](https://i.ytimg.com/vi/_oK9Jd8LH1E/maxresdefault.jpg)

# Fournisseur et création createStore

**Provider” et “createStore()” :** Comme avec connect(), nous devons commencer par envelopper l’intégralité de notre application dans un composant `<Provider>` pour rendre le magasin disponible dans tout le composant.

```
const store = createStore(rootReducer)
ReactDOM.render(
 <Provider store={store}>
   <App />
 </Provider>,
 document.getElementById('root')
```

# utiliserSelector()

### `mapStateToProps`et `connect`argument:

Nous remplaçons notre célèbre argument `mapStateToProps`and `connect`par ce hook sélecteur : `useSelector()`qui nous permet d'extraire des données du magasin d'état Redux.

Il sera appelé avec l'état complet du magasin Redux comme seul argument.

Il sera exécuté à chaque fois que le composant de fonction est rendu (à moins que sa référence n'ait pas changé depuis le rendu précédent du composant, ce qui donne lieu à un ensemble de cache pouvant être renvoyé par le hook sans réexécuter le sélecteur).

**useSelector()** s'abonne également au magasin Redux et exécute notre sélecteur chaque fois qu'une action est envoyée.

Avec `mapStateToProps`, tous les champs individuels sont renvoyés dans un objet combiné. Peu importe que l'objet renvoyé soit une nouvelle référence ou non. connect() compare simplement les champs individuels. Avec `useSelector()`, renvoyer un nouvel objet à chaque fois forcera toujours un nouveau rendu par défaut. Si vous souhaitez récupérer plusieurs valeurs du magasin.

Lors de l'utilisation `useSelector`d'un sélecteur en ligne, une nouvelle instance du sélecteur est créée chaque fois que le composant est rendu.

Cela fonctionne tant que le sélecteur ne conserve aucun état. Cependant, les sélecteurs mémorisants (par exemple créés via `useSelector()`from reselect) ont un état interne et c'est pourquoi ils doivent être utilisés avec précaution.
Lorsque le sélecteur ne dépend que de l'état, assurez-vous qu'il est déclaré en dehors du composant afin que la même instance de sélecteur soit utilisée pour chaque rendu.

# useSelector(): exemple

**Exemple** : Dans l’exemple ci-dessous, nous allons utiliser le `createSelector`nad `useSelector`.

```
import React from "react";
import { useSelector } from "react-redux";
import { createSelector } from "reselect";

const selectNumOfDoneTodos = createSelector(
 state => state.todos,
 todos => todos.filter(todo => todo.isDone).length
);

export const DoneTodosCounter = () => {
 const NumOfDoneTodos = useSelector(selectNumOfDoneTodos);
 return <div>{NumOfDoneTodos}</div>;
};

export const App = () => {
 return (
   <>
     <span>Number of done todos:</span>
     <DoneTodosCounter />
   </>
 );
};
```

# useDispatch()

**mapDispatchToProps :** cette fonction est remplacée par une fonction **« useDispatch »** . Cette fonction renvoie une référence à la fonction de répartition du magasin Redux. Nous pouvons l'utiliser pour répartir les actions selon les besoins.

```
import React from "react";
import { useDispatch } from "react-redux";

export const CounterComponent = ({ value }) => {
 const dispatch = useDispatch();

 return (
   <div>
     <span>{value}</span>
     <button onClick={() => dispatch({ type: "increment-counter" })}>
       Increment counter
     </button>
   </div>
 );
};
```

# useCallback()

Transmettez un rappel en ligne et un tableau de dépendances. `useCallback`renverra une version mémorisée du rappel qui ne change que si l'une des dépendances a changé.
Ceci est utile lors de la transmission de rappels à des composants enfants optimisés qui s'appuient sur l'égalité des références pour éviter les rendus inutiles.

```
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

# Contexte personnalisé

Le `<Provider>`composant nous permet de spécifier un contexte alternatif via la propriété context. Cela est utile si nous créons un composant réutilisable complexe et que nous ne voulons pas que notre boutique entre en conflit avec une boutique Redux que les applications de nos consommateurs pourraient utiliser.

Pour accéder à un contexte alternatif via l'API des hooks, utilisez les fonctions de création de hooks :

```
import React from "react";
import {
 Provider,
 createStoreHook,
 createDispatchHook,
 createSelectorHook
} from "react-redux";

const MyContext = React.createContext(null);

// Export your custom hooks if you wish to use them in other files.
export const useStore = createStoreHook(MyContext);
export const useDispatch = createDispatchHook(MyContext);
export const useSelector = createSelectorHook(MyContext);

const myStore = createStore(rootReducer);

export function MyProvider({ children }) {
 return (
   <Provider context={MyContext} store={myStore}>
     {children}
   </Provider>
 );
}
```

### Ces ressources peuvent vous aider

Hooks redux

[https://medium.com/better-programming/how-to-use-redux-with-react-hooks-5422a7ceae6e](https://medium.com/better-programming/how-to-use-redux-with-react-hooks-5422a7ceae6e)

useSelector() et useDispatch()

[https://levelup.gitconnected.com/react-redux-hooks-useselector-and-usedispatch-f7d8c7f75cdd](https://levelup.gitconnected.com/react-redux-hooks-useselector-and-usedispatch-f7d8c7f75cdd)
