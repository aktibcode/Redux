# Chapitre : LE REDUCTEUR


# Créer un réducteur

Qu'est-ce qu'un réducteur ?
Un réducteur Redux est simplement une **fonction JavaScript** . Il **prend deux paramètres** : l'état actuel et l'action.

Dans un composant React typique, l'état local peut être muté sur place. Dans Redux, vous n'êtes pas autorisé à faire cela. Le **troisième principe de Redux (tel que décrit par son créateur) prescrit que l'état est immuable et ne peut pas changer sur place** .

En d'autres termes, le réducteur doit être **pur** . Une fonction pure renvoie la même sortie pour l'entrée donnée. Malgré cette terminologie, le raisonnement sur un **réducteur n'est pas si difficile.**

# Créer un réducteur

Dans notre exemple, nous allons créer un réducteur simple qui prend l'état initial et l'action comme paramètres.
Créez un nouveau fichier sous le dossier Reducers nommé rootReducer.js.

**src/JS/Reducers/rootReducer.js** c'est le chemin pour le fichier de création

```
const initialState = {
 counter: 0
};

function rootReducer(state = initialState, action) {
 return state;
};

export default rootReducer;
```

### Ces ressources peuvent vous aider

Créer une boutique

[https://redux.js.org/api/createstore](https://redux.js.org/api/createstore)
