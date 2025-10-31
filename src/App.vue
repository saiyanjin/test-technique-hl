<template>
  <div id="app">
    <contextmenu>
      <p>
        Maître Corbeau, sur un arbre perché,<br>
        Tenait en son bec un fromage.<br>
        Maître Renard, par l'odeur alléché,<br>
        Lui tint à peu près ce langage :<br>
        Et bonjour, Monsieur du Corbeau.<br>
        Que vous êtes joli ! que vous me semblez beau !<br>
        Sans mentir, si votre ramage<br>
        Se rapporte à votre plumage,<br>
        Vous êtes le Phénix des hôtes de ces bois.<br>
        À ces mots, le Corbeau ne se sent pas de joie ;<br>
        Et pour montrer sa belle voix,<br>
        Il ouvre un large bec, laisse tomber sa proie.<br>
        Le Renard s'en saisit, et dit : Mon bon Monsieur,<br>
        Apprenez que tout flatteur<br>
        Vit aux dépens de celui qui l'écoute.<br>
        Cette leçon vaut bien un fromage, sans doute.<br>
        Le Corbeau honteux et confus<br>
        Jura, mais un peu tard, qu'on ne l'y prendrait plus.
      </p>
    </contextmenu>
  </div>
</template>

<script setup lang="ts">
import Contextmenu from "./components/Contextmenu.vue";
</script>

<style>
html,
body,
#app {
  margin: 0;
  height: 100%;
  width: 100%;
}

#app {
  position: relative;
}
</style>