# Vue Starter

- [Vue 3](https://vuejs.org/)
- [VueUse](https://vueuse.org/)
- [Pinia](https://pinia.vuejs.org/)
- [Vue Router](https://router.vuejs.org/)

## Project Setup

```sh
yarn install
yarn run dev
```

## Routing

VueRouter is configured through the `unplugin-vue-router` plugin.

Just add your pages in the `src/pages` folder, and they will be automatically imported and added to the router.

# Sandwich Generator

## Mandatory Features
- Button "Générer un sandwich" generates a random sandwich from predefined ingredients
- Generated sandwich is displayed on screen
- Button "Sauvegarder" adds the sandwich to a saved list
- Saved list is displayed on the same page
- Each sandwich has a delete button to remove it from the list

## Bonus Features
- Anti-doublon : cannot save the same sandwich twice
- Compteur : total number of saved sandwiches is displayed
- Filtre : saved sandwiches can be filtered, but only by bread type
- Design : some css was added, but not much

