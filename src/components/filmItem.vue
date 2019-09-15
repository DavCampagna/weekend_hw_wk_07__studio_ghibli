<template lang="html">
  <div>
    <p v-on:click="showFilmInfo">{{film.title}}</p>
      <button v-on:click="addFavourite">Add to Favourites</button>
      <button v-on:click="removeFavourite">Remove from Favourites</button>

  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: "film-item",
  props: ["film"],
  methods: {
  showFilmInfo(){
    eventBus.$emit('film-selected', this.film)
    },
  addFavourite(){
    eventBus.$emit('favourite-added', this.film)
    },
  removeFavourite(){
    eventBus.$emit("favourite-removed", this.film);
    }
  }
}
</script>

<style lang="css" scoped>

p{
  color: darkblue;
  font-family: cursive;
  font-size: 25px;
  text-align: left;
}

</style>
