# Chapitre : LA BIBLIOTHEQUE REACT-REDUX


# Qu'est-ce que React-redux

React Redux est la bibliothèque officielle de liaison d'interface utilisateur Redux pour React. Si vous utilisez Redux et React ensemble, vous devez également utiliser React-Redux pour lier ces deux bibliothèques.
En tant que liaison Redux officielle pour React, React-Redux est tenu à jour avec toutes les modifications d'API de l'une ou l'autre bibliothèque pour garantir que vos composants React se comportent comme prévu. Son utilisation prévue adopte les principes de conception de React - écriture de composants déclaratifs. Voici quelques avantages de l'utilisation de la bibliothèque React-Redux

* **Cela encourage une bonne architecture React :** en tant que principe architectural général, nous voulons que nos propres composants ne soient pas « conscients » de Redux. Ils doivent simplement recevoir des données et des fonctions en tant qu'accessoires, comme tout autre composant React. Cela facilite en fin de compte le test et la réutilisation de vos propres composants.
* **Il implémente des optimisations de performances :** React Redux implémente de nombreuses optimisations de performances en interne, de sorte que votre propre composant ne s'affiche à nouveau que lorsqu'il en a réellement besoin.
* **Assistance communautaire :** en tant que bibliothèque de liaison officielle pour React et Redux, React Redux dispose d'une large communauté d'utilisateurs. Cela permet de demander plus facilement de l'aide, de se renseigner sur les meilleures pratiques, d'utiliser des bibliothèques qui s'appuient sur React Redux et de réutiliser vos connaissances dans différentes applications.

# Redux contre React-Redux

**Redux** vous offre un magasin et vous permet de conserver les états et de les extraire. Il répond lorsque l'état change. mais c'est tout ce qu'il fait.

C'est en fait **React-Redux** qui vous permet de connecter des morceaux de l'état aux composants React.

C'est vrai : **Redux** ne sait rien du tout de React.

Ces bibliothèques sont comme deux petits pois dans une cosse. 99,999 % du temps, lorsque quelqu'un mentionne « Redux » dans le contexte de React, il fait référence à ces deux bibliothèques en tandem. C'est donc ce que vous devez garder à l'esprit lorsque vous voyez Redux mentionné sur StackOverflow, Reddit ou n'importe où ailleurs.

La bibliothèque **redux** peut également être utilisée en dehors d'une application React. Elle fonctionnera avec Vue, Angular et même avec les applications backend Node/Express.

# Installation de React-Redux

Pour commencer à utiliser Redux avec React, il vous suffit de suivre ces étapes :

1. Créer une nouvelle application React
   ```
   $ npx create-react-app react-redux-counter
   ```
2. Installer redux
   ```
   $ npm i redux
   ```
3. installer react-redux
   ```
   $ npm i react-redux
   ```

# Architecture des dossiers Redux

Redux peut rendre votre vie de développeur beaucoup plus facile ou beaucoup plus difficile en fonction de l'architecture que vous suivez.
En cherchant sur le Web, vous pouvez trouver de nombreuses architectures ou méthodes différentes pour implémenter Redux dans votre application React. Voici celle que nous vous recommandons d'utiliser.

![](https://i.imgur.com/kv7USWC.png)

Cette architecture est simple et organisée. Vous devez créer un dossier appelé JS (ou tout autre nom que vous préférez).
Sous le dossier JS, il y aura quatre sous-dossiers :
-> **Actions** : Ce dossier contiendra toutes les actions
-> **Constantes** : Ce dossier inclura tous les créateurs d'actions
-> **Réducteurs** : il contiendra les réducteurs
-> **Store** : il contiendra la création du store.

### Ces ressources peuvent vous aider

Installation de Redux

[https://redux.js.org/introduction/installation](https://redux.js.org/introduction/installation)

React-Redux

[https://react-redux.js.org/introduction/quick-start](https://react-redux.js.org/introduction/quick-start)
