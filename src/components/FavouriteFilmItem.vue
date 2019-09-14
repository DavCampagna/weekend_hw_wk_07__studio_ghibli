<template lang="html">
  <li>
    {{ film.name }}
    <button v-on:click="selectFilm">Display Info</button>
    <button v-on:click="removeFavourite">Remove from Favourites</button>
  </li>
</template>

<script>
import { eventBus } from "@/main";

export default {
  name: "favourite-film-item",
  props: ["film"],
  methods: {
    selectFilm: function() {
      eventBus.$emit("film-selected", this.film);
    },
    removeFavourite: function() {
      eventBus.$emit("favourite-removed", this.film);
    }
  }
};
</script>

<style lang="css" scoped>
</style>
