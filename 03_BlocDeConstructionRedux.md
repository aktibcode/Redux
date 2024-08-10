# Chapitre : BLOC DE CONSTRUCTION DE REDUX


# Qu'est-ce qu'une action ?

Plongeons plus en profondeur dans les éléments constitutifs de Redux.
Les actions sont des objets JavaScript comme vous pouvez le voir dans l'exemple suivant :

```
{
   type: LOGIN_USER,
   payload: {
     username: 'sebastian',
      password: '123456'
      }
}
```

Ici, l'objet action a deux propriétés :

* *type :* une constante pour identifier le type d'action.
* *charge utile :* l'objet qui est affecté à cette propriété contient les données qui sont envoyées au magasin.

Les objets d'action sont créés à l'aide de fonctions. Ces fonctions sont appelées créateurs d'actions

```
function authUser(data) {
 return {
   type: LOGIN_USER,
   payload: data,
 };
}
```

Ici, vous pouvez voir que le seul but d'une fonction de création d'action est de renvoyer l'objet d'action tel que décrit.
L'appel d'actions dans l'application est facile en utilisant la méthode de répartition :
`dispatch(authUser(data));`

# Qu'est-ce qu'un réducteur ?

Les réducteurs sont les éléments de base les plus importants et il est important de comprendre le concept. Les réducteurs sont des fonctions JavaScript pures qui prennent l'état actuel de l'application et un objet d'action et renvoient un nouvel état de l'application :

```
const reducer = (state, action) => {
switch (action.type) {
 case type1:
   return; // the new state
case type2:
   return; // the new state
 default:
   return state;
}

}
```

Il est important de noter ici que l'état n'est pas modifié directement. Au lieu de cela, un nouvel objet d'état (basé sur l'ancien état) est créé et la mise à jour est effectuée vers le nouvel état.

# Qu'est-ce que le Redux Store ?

Le magasin est l'objet central qui contient l'état de l'application. Le magasin est créé à l'aide de la `createStore`méthode de la bibliothèque Redux :

```
import { createStore } from ‘redux’;
let store = createStore(myReducer);

```

Vous devez transmettre la fonction de réduction en tant que paramètre. Vous êtes maintenant prêt à envoyer une action au magasin qui est gérée par le réducteur :

# Flux de données Redux

L'image ci-dessous décrit le flux de données Redux et la manière dont chaque partie est déclenchée :

![](https://i.imgur.com/acGRCwx.png)

### Ces ressources peuvent vous aider

Mieux comprendre Redux

[https://www.youtube.com/watch?time_continue=37&amp;v=3sjMRS1gJys&amp;feature=emb_title](https://www.youtube.com/watch?time_continue=37&v=3sjMRS1gJys&feature=emb_title)
