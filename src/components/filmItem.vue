<template lang="html">
  <div>
    <h2 v-on:click="showFilmInfo">{{film.title}}</h2>
    <button v-if="!isFavourite" v-on:click="addFavourite">Add to Favourites</button>
    <button v-if="isFavourite" v-on:click="removeFavourite">Remove from Favourites</button>
    <button v-if="!hasBeenWatched" v-on:click="addWatched">Mark as Watched</button>
    <p v-if="hasBeenWatched">Watched!</p>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: "film-item",
  props: ["film", "isFavourite", "hasBeenWatched"],
  methods: {
  showFilmInfo(){
    eventBus.$emit('film-selected', this.film)
    },
  addFavourite(){
    eventBus.$emit('favourite-added', this.film)
    },
  removeFavourite(){
    eventBus.$emit("favourite-removed", this.film);
    },
  addWatched(){
    eventBus.$emit("film-watched", this.film)
    }
  }
}
</script>

<style lang="css" scoped>

h2{
  color: darkblue;
  font-family: cursive;
  font-size: 25px;
  text-align: left;
}

</style>
