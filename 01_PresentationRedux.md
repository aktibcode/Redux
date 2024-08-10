# Chapitre : PRESENTATION DE REDUX


# Introduction

L'une des fonctionnalités fournies par React est le flux de données unidirectionnel. Bien que cette fonctionnalité puisse aider les développeurs à déboguer et à suivre les données, lorsque nous en arrivons à la gestion des états (en particulier lorsque l'application grandit au fil du temps), elle peut ouvrir la porte de l'enfer.

Redux est l'une des bibliothèques de gestion d'état les plus connues et les plus utilisées. La gestion des états avec Redux sera notre principal intérêt dans cette Super Skill. Voici ce que nous allons voir :

* Qu'est-ce que Redux ?
* Le mécanisme que Redux utilise pour gérer les états.
* Intergiciel Redux.
* Redux avec des crochets.

# Gérer les états avec React

Par définition, un état est un objet qui définit l'état actuel de notre application.
Étant donné que React est une bibliothèque d'interface utilisateur basée sur des composants, qui utilise l'état pour suivre les parties mobiles de l'interface utilisateur, la gestion de l'état dans les applications est très importante à comprendre.
React permet aux développeurs d'utiliser l'état au niveau des composants en utilisant des composants basés sur des classes ou des composants basés sur des fonctions.

# Le problème de la gestion de l’État

Étant donné que l'état d'un composant peut être transmis dans des props, cela devient rapidement déroutant. Par exemple, si vous devez transmettre l'état au plus profond d'une arborescence de composants à un enfant, vous devez le transmettre à chaque composant intermédiaire. C'est ce qu'on appelle **le prop-drilling** , et il devient de plus en plus difficile de suivre votre état ou de modifier un code à l'avenir, car cela devient un processus fastidieux.
Pour résoudre le problème du prop-drilling, les développeurs travaillant avec React utilisent souvent une sorte d'outil de gestion d'état. C'est là que de nombreuses personnes passent à Redux pour gérer l'état.
![](https://i.imgur.com/zYmBnDa.png)

# Démarrer avec Redux

Pour résoudre le problème du forage des propriétés, les développeurs qui travaillent avec React utilisent souvent une sorte d'outil de gestion d'état. C'est là que de nombreuses personnes se tournent vers Redux pour gérer l'état.
À première vue, Redux semble complexe et absolument inutile. Certaines des questions que de nombreux nouveaux développeurs se posent lorsqu'ils apprennent Redux sont : « Pourquoi ai-je besoin de séparer mon état ? » et « Quels sont tous ces nouveaux termes et comment ma structure de dossiers est-elle devenue si désordonnée ? »

Mais une fois que vous aurez compris le concept de base de Redux, ce sera la solution à tous les problèmes de gestion d'état.

### Ces ressources peuvent vous aider

Pourquoi avons-nous besoin de Redux ?

[https://blog.logrocket.com/why-use-redux-reasons-with-clear-examples-d21bffd5835/#:~:text=Redux%20makes%20it%20easy%20to,the%20state%20of%20pure% 20 fonctions.](https://blog.logrocket.com/why-use-redux-reasons-with-clear-examples-d21bffd5835/#:~:text=Redux%20makes%20it%20easy%20to,the%20state%20of%20pure%20functions.)

Gestion des états dans React

[https://medium.com/dailyjs/comparison-of-state-management-solutions-for-react-2161a0b4af7b](https://medium.com/dailyjs/comparison-of-state-management-solutions-for-react-2161a0b4af7b)
