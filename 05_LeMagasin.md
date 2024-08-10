# Chapitre : LE MAGASIN


# Créer la boutique

Le magasin est celui qui est responsable de l'orchestration des rouages. Le magasin dans Redux est une sorte de magie et contient tout l'état de l'application.

Créons un magasin pour commencer à jouer avec Redux. Sous le dossier du magasin, créez un nouveau fichier index.js, chemin vers le fichier ***src/js/store/index.js*** et initialisez le magasin.

```
// src/js/store/index.js

import { createStore } from "redux";
import rootReducer from "../reducers/rootReducer";

const store = createStore(rootReducer);

export default store;

```

Comme vous pouvez le voir, store est le résultat de l'appel à createStore, une fonction de la bibliothèque Redux. createStore prend un réducteur comme premier argument et dans notre cas, nous avons passé rootReducer (pas encore présent).
Le concept le plus important à comprendre ici est que l'état dans Redux provient des réducteurs.

# fonction createStore

```
createStore(reducer, [preloadedState], [enhancer])
```

Crée un magasin Redux qui contient l'arborescence d'état complète de votre application. Votre application ne doit contenir qu'un seul magasin.

Arguments:

1. **Réducteur** : (Fonction) : Une fonction réductrice qui renvoie l'arbre d'état suivant, étant donné l'arbre d'état actuel et une action à gérer.
2. **[preloadedState]** : l'état initial. Vous pouvez éventuellement le spécifier pour hydrater l'état à partir du serveur dans les applications universelles.
3. **[enhancer]** : L'améliorateur de magasin. Vous pouvez éventuellement le spécifier pour améliorer le magasin avec des fonctionnalités tierces telles que le middleware, le voyage dans le temps, la persistance, etc.

> les arguments placés entre [ ] signifient que ces arguments sont facultatifs.

La fonction createStore renvoie un store (un objet qui contient l'état complet de votre application.

### Ces ressources peuvent vous aider

État global

[https://github.com/benhurott/react-create-global-state](https://github.com/benhurott/react-create-global-state)
