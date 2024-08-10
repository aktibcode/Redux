# Chapitre : EXEMPLE


# Exemple

Au cours de cette compétence, nous allons explorer un exemple en partant de zéro. Pour voir la situation dans son ensemble.
Tout d'abord, commençons par créer notre application React

```
$ npx create-react-app blog
```

Définissons maintenant l'arborescence des composants, nous allons créer un composant de dossier qui contient le composant que nous utilisons

sous src/component créez ces fichiers PostList.js et CreatePost.js
PostList recevra la liste des articles du magasin et CreatePost.js ajoutera de nouveaux articles dans le magasin.

```
//PostList.js
import React from 'react'

const PostList = (props) => {
    return (
        <div>
            {props.posts.map((post) => <div id={post.id}>
                <h1>{post.title}</h1>
                <p>{post.content}</p>
            </div>)}
        </div>
    )
}

export default PostList
```

```
//CreatePost.js
import React, { useState } from 'react'

const CreatePost = () => {
    const [title, setTitle] = useState('')
    const [content, setContent] = useState('');
    const handleSubmit = (e) => {
        e.preventDefault()
    }
    return (
        <form onSubmit={handleSubmit}>
            <div>

                <label htmlFor="Title">Title</label>
                <input type="text" name="title" id="title" onChange={e => setTitle(e.target.value)} />
            </div>
            <div>
                <label htmlFor="Content">Content:</label>
                <textarea name="content" id="content" cols="30" rows="10" onChange={e => setContent(e.target.value)} />
            </div>
            <div>
                <input type="submit" value="Add" />
            </div>


        </form>
    )
}

export default CreatePost
```

```
//App.js
import CreatePost from './Components/CreatePost';
import PostList from './Components/PostList';

function App() {

  return (
    <div className="App">
      <CreatePost/>
      <PostList/>
    </div>
  );
}

export default App;
```

# Configuration Redux

Pour commencer à travailler avec Redux, nous commençons d'abord par installer la bibliothèque React et React-Redux

```
$ npm i redux react-redux 
```

Ensuite, nous allons suivre l’architecture dont nous avons parlé dans les diapositives précédentes.

```
//src/JS/store.js
import { createStore } from 'redux'
import rootReducer from '../Reducers/rootReducer'

const store = createStore(rootReducer)
export default store;
```

```
//src/JS/Reducers/rootReducers.js
import { ADD_ARTICLE } from "../Constants/actions-types";

const initialState = {
    posts: [
        {
            id: 1,
            title: 'my first post',
            content: 'my first content'
        }
    ]
}
const rootReducer = (state = initialState, action) => {
    switch (action.type) {
        case ADD_ARTICLE:
            return {
                posts: [...state.posts, action.payload]
            }
        default:
            return state
    }
}

export default rootReducer
```

```
// src/JS/Constants/actions-types.js
export const ADD_ARTICLE = 'ADD_ARTICLE'
```

```
// src/JS/Actions/actions.js
import { ADD_ARTICLE } from "../Constants/actions-types";

export const addPost = newPost => {
    return {
        type: ADD_ARTICLE,
        payload: newPost
    }
}


```

# Connectez l'application React du magasin

Pour connecter le store à votre application React, vous aurez besoin d'un composant de la bibliothèque React-Redux nommé Provider.
Le composant Provider est utilisé pour encapsuler l'application React et lui donnera accès au store.
Pour être sûr que l'application a accès au store, allez-y et modifiez l'index.js de votre application React comme dans l'exemple suivant :

```
//src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { Provider } from 'react-redux';
import store from './JS/store';

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}> {/* the component Provider needs a props store  */}
      <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

Comme vous pouvez le voir dans le code ci-dessus, le composant Provider a besoin d'un accessoire nommé store, à travers cela `props`nous transmettons le redux `store`à la hiérarchie encapsulée (qui dans notre cas, l'ensemble de l'application)

# Connectez le composant pour obtenir l'état

Dans la diapositive précédente, nous avons vu comment rendre le magasin accessible à la hiérarchie. Chaque composant de cette hiérarchie a le droit de se connecter et d'utiliser les données qui existent dans le magasin. Mais cela ne suffit pas. Le composant lui-même doit être connecté au magasin.
La bibliothèque react-redux nous fournit une autre méthode `connect`. Elle fournit à son composant connecté les éléments de données dont il a besoin du magasin et les fonctions qu'il peut utiliser pour envoyer des actions au magasin.
Elle ne modifie pas le composant qui lui est passé ; à la place, elle renvoie une nouvelle classe de composant connecté qui encapsule le composant que vous avez passé.
La syntaxe de la méthode connect peut sembler un peu étrange, mais examinons-la de plus près.

```
connect(mapStateToProps, mapDispatchToProps)(Component)
```

Expliquons-le maintenant :

* `mapStateToProps`: c'est une fonction qui renvoie l'état (ou seulement une partie de l'état) et le transmet au composant en tant qu'accessoire. cette fonction n'est pas fournie par la bibliothèque, elle doit être implémentée par vous.
* `mapDispatchToProps`: il fait quelque chose de similaire, mais pour les actions. mapDispatchToProps connecte les actions Redux aux props React. De cette façon, un composant React connecté pourra envoyer des messages au magasin.
* `Component`:Le composant qui souhaite se connecter au magasin.

Jetons un œil au fichier PostList.js pour mieux comprendre.

```
import React from 'react'
import { connect } from 'react-redux'

const mapStateToProps = state => {
    return {
        posts: state.posts
    }
}
const PostList = (props) => {
    return (
        <div>
            {props.posts.map((post) => <div id={post.id}>
                <h1>{post.title}</h1>
                <p>{post.content}</p>
            </div>)}
        </div>
    )
}

export default connect(mapStateToProps)(PostList)
```

# Gérer les actions

L'étape suivante de notre projet consiste à faire fonctionner le composant CreatePost et à ajouter les nouveaux articles à la boutique. Pour ce faire, nous allons utiliser la fonction mapDispatchToProps, comme illustré dans l'exemple ci-dessous

```
import React, { useState } from 'react'
import { connect } from 'react-redux';
import { addPost } from '../JS/Actions/actions';

const mapDispatchToProps = dispatch => {
    return {
        addArticle: post => dispatch(addPost(post))
    }
}
const CreatePost = (props) => {
    const [title, setTitle] = useState('')
    const [content, setContent] = useState('');
    const handleSubmit = (e) => {
        e.preventDefault()
        props.addArticle({
            id: Date.now(),
            title,
            content
        })
    }
    return (
        <form onSubmit={handleSubmit}>
            <div>

                <label htmlFor="Title">Title</label>
                <input type="text" name="title" id="title" onChange={e => setTitle(e.target.value)} />
            </div>
            <div>
                <label htmlFor="Content">Content:</label>
                <textarea name="content" id="content" cols="30" rows="10" onChange={e => setContent(e.target.value)} />
            </div>
            <div>
                <input type="submit" value="Add" />
            </div>


        </form>
    )
}

export default connect(null, mapDispatchToProps)(CreatePost)
```

Le mapDispatchToProps est le deuxième argument dont la méthode connect a besoin, c'est pourquoi nous avons passé le null au lieu de mapSateToProps, mais les deux méthodes peuvent être passées si nécessaire.

La fonction `mapDispatchToProps`prend comme paramètre `dispatch`et renvoie un objet.

![](https://i.imgur.com/Rio9CY6.png)

1. `addAtricle`: La clé du premier élément de l'objet renvoyé. C'est celle qui sera utilisée dans le composant ( props.AddArticle )
2. fonction : qui prend un message comme argument (le nouveau message à ajouter) et envoie l'action d'ajout de ce nouveau message.

N'hésitez pas à essayer cet exemple par vous-même. Vous pouvez retrouver l'intégralité du projet sur ce [lien](https://github.com/gomycode-engineering/React-Redux-Posts)
