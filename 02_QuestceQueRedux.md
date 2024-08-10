# Chapitre : QU'EST CE QUE REDUX ?


# Qu'est-ce que Redux ?

> Par définition, Redux est un conteneur d’état prévisible pour les applications JavaScript.

En d'autres termes, Redux est une bibliothèque autonome. Elle vous aide à écrire des applications qui se comportent de manière cohérente, s'exécutent dans différents environnements (client, serveur et natif) et sont faciles à tester.
De plus, elle offre une excellente expérience de développement, comme l'édition de code en direct combinée à un débogueur voyageant dans le temps.

![](https://i.imgur.com/eCNHidt.png)

# Principes de Redux

La prévisibilité de Redux est déterminée par les trois principes les plus importants indiqués ci-dessous :

* **Source unique de vérité :** l'état de l'ensemble de votre application est stocké dans une arborescence d'objets au sein d'un magasin unique. Comme l'ensemble de l'état de l'application est stocké dans une arborescence unique, le débogage est plus facile et le développement plus rapide.
* **L'état est en lecture seule :** la seule façon de modifier l'état est d'émettre une action, un objet décrivant ce qui s'est passé. Cela signifie que personne ne peut modifier directement l'état de votre application.
* **Les modifications sont effectuées avec des fonctions pures :** pour spécifier comment l'arbre d'état est transformé par les actions, vous écrivez des réducteurs purs. Un réducteur est un endroit central où la modification d'état a lieu. Le réducteur est une fonction qui prend l'état et l'action comme arguments et renvoie un état nouvellement mis à jour.

![](https://i.imgur.com/AMPOSnm.png)

# Comment fonctionne Redux ?

Pour bien comprendre le concept de Redux, nous devons d'abord examiner le bloc de construction man. Redux comporte trois parties principales : les actions, les réducteurs et le magasin. Explorons ce que fait chacune d'elles :

* **Actions :** elles permettent d'envoyer des informations de l'application au magasin. L'envoi de données au magasin est nécessaire pour modifier l'état de l'application après une interaction avec l'utilisateur, des événements internes ou des appels d'API.
* **Réducteurs :** sont les éléments de base les plus importants et il est important de comprendre le concept.
* **Magasin :** Le magasin est l'objet central qui contient l'état de l'application.

Pour faciliter la compréhension, imaginons ce scénario, le composant déclenche une action pour modifier la valeur de l'état global. L'action est envoyée au magasin. Le magasin appelle le réducteur pour créer un nouvel état basé sur l'action envoyée. Lorsque le nouvel état est créé, le composant met à jour sa vue.

![](https://i.imgur.com/EXUOLg6.png)

### Ces ressources peuvent vous aider

Démarrer avec Redux

[https://redux.js.org/introduction/getting-started](https://redux.js.org/introduction/getting-started)
