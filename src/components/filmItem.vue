<template lang="html">
  <div>
    <h2 v-on:click="showFilmInfo">{{film.title}}</h2>
    <!-- <button v-if="!showDetail" v-on:click="showFilmInfo">Show Info</button> -->

    <p v-if="isFavourite">Favourite!</p>
    <p v-if="hasBeenWatched, !addFavourite">Watched!</p>
    <button v-if="isFavourite" v-on:click="removeFavourite">Remove from Favourites</button>
    <button v-if="!isFavourite" v-on:click="addFavourite">Add to Favourites</button>
    <button v-if="!hasBeenWatched" v-on:click="addWatched">Mark as Watched</button>
    <button v-if="!isWatchlistItem, !hasBeenWatched" v-on:click="addToWatchlist">Add to Watchlist</button>
    <button v-if="isWatchlistItem" v-on:click="removeWatchlistItem">Remove from Watchlist</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: "film-item",
  props: ["film", "isFavourite", "hasBeenWatched", "isWatchlistItem", "showDetail"],
  methods: {
  showFilmInfo(){
    eventBus.$emit("film-selected", this.film)
    },
  unselectFilm(){
    eventBus.$emit("film-unselected", this.film)
    },
  addFavourite(){
    eventBus.$emit('favourite-added', this.film)
    },
  removeFavourite(){
    eventBus.$emit("favourite-removed", this.film);
    },
  addWatched(){
    eventBus.$emit("film-watched", this.film)
    },
  addToWatchlist(){
    eventBus.$emit("watchlist-added", this.film)
    },
  removeWatchlistItem(){
    eventBus.$emit("watchlist-removed", this.film)
    },
  addToWatchAgain(){
    eventBus.$emit("watchAgain-added", this.film)
    }
  }
}
</script>

<style lang="css" scoped>

h2{
  color: darkmagenta;
  text-shadow:5px 5px 10px white;
  font-family: cursive;
  font-size: 28px;
}

div{
  text-align: center;
  padding: 20px;
}

div:hover{
  color: magenta;
  cursor: default;
  background-color: hsla(60, 92%, 72%, 0.49);
  border-radius: 15px;
  padding: 20px;
}
</style>
