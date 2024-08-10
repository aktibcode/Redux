# Chapitre : BOITE A OUTILS REDUX

# Qu'est-ce que Redux-toolkit ?

React et Redux étaient considérés comme la meilleure combinaison pour gérer l'état dans les applications React à grande échelle. Cependant, la configuration et le code source extrêmement requis ont rendu la compréhension et la manipulation un peu difficiles.
C'est là qu'est venu le rôle de la boîte à outils Redux.
Redux-toolkit est une nouvelle façon d'implémenter Redux, une façon plus fonctionnelle. C'est plus propre, vous écrivez moins de lignes de code et nous obtenons la même gestion d'état Redux, que nous aimons et à laquelle nous faisons confiance. Le meilleur, c'est qu'il est `redux-thunk `déjà intégré. De plus, ils gèrent `immerJs` toute l'immuabilité, donc tout ce à quoi nous devons penser est ce qui doit être fait.

![](https://i.imgur.com/o9slFZc.png)

# Principales caractéristiques de Redux Tool Kit

La fonction suivante est utilisée par Redux Took Kit, qui est un résumé de la fonction Redux existante. Ces fonctions ne modifient pas le flux de Redux mais les rationalisent seulement de manière plus lisible et plus gérable.

* **configureStore** : crée une instance de magasin Redux comme le createStore d'origine de Redux, mais accepte un objet d'options nommé et configure automatiquement l'extension Redux DevTools.
* **createAction** : accepte une chaîne de type d'action et renvoie une fonction de création d'action qui utilise ce type.
* **createReducer** : accepte une valeur d'état initiale et une table de recherche de types d'actions pour les fonctions de réduction et crée un réducteur qui gère tous les types d'actions.
* **createSlice** : accepte un état initial et une table de recherche avec des noms et des fonctions de réduction et génère automatiquement des fonctions de création d'action, des chaînes de type d'action et une fonction de réduction.

Vous pouvez utiliser la fonction ci-dessus pour simplifier le code standard dans Redux, en particulier à l'aide des méthodes createAction et createReducer. Cependant, cela peut être encore plus simplifié à l'aide de createSlice, qui génère automatiquement des fonctions de création et de réduction d'actions.

# Qu'est-ce qui est si spécial à propos de createSlice ?

Il s'agit d'une fonction d'assistance qui génère une tranche de magasin. Elle prend le nom de la tranche, l'état initial et la fonction de réduction pour renvoyer le réducteur, les types d'action et les créateurs d'action.
Tout d'abord, voyons à quoi ressemblent les réducteurs et les actions dans les applications React-Redux traditionnelles.

* **Actions**

```
import {GET_USERS,CREATE_USER,DELETE_USER} from "../constant/constants";
export const GetUsers = (data) => (dispatch) => {
 dispatch({
  type: GET_USERS,
  payload: data,
 });
};
export const CreateUser = (data) => (dispatch) => {
 dispatch({
  type: CREATE_USER,
  payload: data,
 });
};
export const DeleteUser = (data) => (dispatch) => {
 dispatch({
  type: DELETE_USER,
  payload: data,
 });
};
```

* **Reducers**

```
import {GET_USERS,CREATE_USER,DELETE_USER} from "../constant/constants";
const initialState = {
 errorMessage: "",
 loading: false,
 users:[]
};
const UserReducer = (state = initialState, { payload }) => {
switch (type) {
 case GET_USERS:
  return { ...state, users: payload, loading: false };
case CREATE_USER:
  return { ...state, users: [payload,...state.users],
 loading: false };
case DELETE_USER:
  return { ...state, 
  users: state.users.filter((user) => user.id !== payload.id),
, loading: false };
default:
  return state;
 }
};
export default UserReducer;
```

Voyons maintenant comment nous pouvons simplifier et obtenir la même fonctionnalité en utilisant `createSlice`.

```
import { createSlice } from '@reduxjs/toolkit';
export const initialState = {
  users: [],
  loading: false,
  error: false,
};
const userSlice = createSlice({
  name: 'user',
  initialState,
  reducers: {
    getUser: (state, action) => {
      state.users = action.payload;
      state.loading = true;
      state.error = false;
    },
    createUser: (state, action) => {
      state.users.unshift(action.payload);
      state.loading = false;
    },
    deleteUser: (state, action) => {
      state.users.filter((user) => user.id !== action.payload.id);
      state.loading = false;
    },
  },
});
export const { createUser, deleteUser, getUser } = userSlice.actions;
export default userSlice.reducer;
```

Comme vous pouvez le voir maintenant, toutes les actions et réducteurs sont dans un endroit simple où une application redux traditionnelle vous oblige à gérer chaque action et son action correspondante à l'intérieur du réducteur. Lorsque vous l'utilisez, `createSlice`vous n'avez pas besoin d'utiliser un commutateur pour identifier l'action.
Lorsqu'il s'agit de muter l'état, un flux Redux typique génère des erreurs et vous aurez besoin de tactiques JavaScript spéciales comme `spread operator`et `Object assign`pour les surmonter. Étant donné que la boîte à outils Redux utilise `Immer`, vous n'avez pas à vous soucier de muter l'état. Étant donné qu'une tranche crée les actions et les réducteurs, vous pouvez les exporter et les utiliser dans votre composant et dans Store pour configurer Redux sans avoir de fichiers et de répertoires séparés pour les actions et les réducteurs comme ci-dessous.

```
import { configureStore } from "@reduxjs/toolkit";
import userSlice from "./features/user/userSlice";
export default configureStore({
 reducer: {
  user: userSlice,
 },
});
```

### Ces ressources peuvent vous aider

React-redux

[https://react-redux.js.org/](https://react-redux.js.org/)
