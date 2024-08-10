# Chapitre : LES ACTIONS


# La nécessité d'agir

Les réducteurs Redux sont sans aucun doute le concept le plus important de Redux. Les réducteurs produisent l'état d'une application.

Mais comment un réducteur sait-il quand générer l’état suivant ?

Le deuxième principe de Redux dit que la seule façon de changer l'état est d'envoyer un signal au magasin. Ce signal est une action. Donc, « **envoyer une action** » signifie **envoyer un signal** au magasin.
Ce qui est rassurant, c'est que les actions Redux ne sont rien d'autre que des objets JavaScript. Voici à quoi ressemble une action :

```
type: "INCREMENT_COUNTER",
 payload: {
   value: 1
 }
```

La propriété ***type*** détermine la manière dont l'état doit changer et elle est toujours requise par Redux. La propriété ***payload*** décrit plutôt ce qui doit changer et peut être omise si vous n'avez pas de nouvelles données à enregistrer dans le magasin.

# Créer des actions :

En tant que bonne pratique dans Redux, nous enveloppons chaque action dans une fonction, de sorte que la création d'objet soit abstraite. Une telle fonction prend le nom de créateur d'action : rassemblons le tout en créant un créateur d'action simple.

Dans le répertoire Actions, créez un fichier nommé actions.js

```
// src/Actions/actions.js

export const incrementCounter = (payload) => ({
 type: "INCREMENT_COUNTER",
 payload 
});
```

# Créer des actions

Vous pouvez remarquer que la propriété type est une chaîne. Les chaînes sont sujettes aux fautes de frappe et aux doublons et pour cette raison, il est préférable de déclarer les actions comme des constantes. C'est ici qu'intervient le rôle des constantes du répertoire. Sous ce dossier, créez un nouveau fichier `actions-types.js`

```
// src/js/constants/action-types.js
export const INCREMENT_COUNTER = "INCREMENT_COUNTER";
```

Ouvrez maintenant à nouveau src/js/Actions/actions.js et mettez à jour l'action pour utiliser les types d'action :

```
// src/Actions/actions.js

import { INCREMENT_COUNTER } from "../constants/actions-types";

export const incrementCounter = (payload) => ({
 type: INCREMENT_COUNTER,
 payload
}
```

# Refactorisation du réducteur

Lorsqu'une action est envoyée, le magasin transmet un message (l'objet d'action) au réducteur. À ce stade, le réducteur vérifie le type de cette action. Ensuite, en fonction du type d'action, le réducteur produit l'état suivant, fusionnant finalement la charge utile de l'action dans le nouvel état.

Réparons notre `rootReducer.js`

```

import { INCREMENT_COUNTER } from "../constants/actions-types";

const initialState = {
  counter: 0
};

function rootReducer(state = initialState, action) {
switch (action.type) {
  case INCREMENT_COUNTER:
  
  return {
    counter : state.counter + 1 
  }
  return state;
};

export default rootReducer;
```

### Ces ressources peuvent vous aider

Réducteurs

[https://redux.js.org/basics/reducers](https://redux.js.org/basics/reducers)
