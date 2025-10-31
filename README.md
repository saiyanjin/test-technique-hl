# test-technique-hl

# Exercices Vue 3

Ce dépôt contient deux exercices pratiques réalisés avec **Vue 3**, **Composition API** et **TypeScript**.

---

## Exercice 1 : International Phone Number

**Objectif :**  
Créer un champ de formulaire pour renseigner un numéro de téléphone avec son `country code`.

**Fonctionnalités :**  
- Composant `InternationalPhoneNumber` réutilisable.
- Communication bidirectionnelle avec le parent via `v-model` multiples.
- Synchronisation entre :
  - `countryCode`  
  - `phoneNumber`  
  - `internationalPhoneNumber`  
- Gestion des événements `@update:country-code` et `@update:phone-number`.
- Parsing automatique du numéro international pour mise à jour des champs individuels.
- Champs limités (`maxlength`) et stylisés avec focus.

**Technologies :**  
- Vue 3 Composition API  
- TypeScript  
- `ref` et `watch` pour la réactivité  

---

## Exercice 2 : Context Menu Wiktionary

**Objectif :**  
Créer un menu contextuel qui s’affiche à la position du curseur et récupère la définition du mot sélectionné depuis l’API Wiktionary.

**Fonctionnalités :**  
- Menu contextuel dynamique positionné selon le curseur.
- Sélection du mot via `window.getSelection()`.
- Appel asynchrone à l’API Wiktionary avec gestion des états :
  - Chargement  
  - Définitions multiples  
  - Erreurs ou absence de définition
- Fermeture du menu au clic ailleurs.
- Réactivité avec `ref` pour coordonnées, visibilité et contenu du menu.

**Technologies :**  
- Vue 3 Composition API  
- TypeScript  
- Gestion des événements et asynchrone  

---

## Structure du projet



