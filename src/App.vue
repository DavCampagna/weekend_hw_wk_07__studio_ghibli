<template lang="html">
  <div id="app">
    <header>
      <!-- <component is="film-list"></component> -->
      <!-- <favourite-film-list v-on:click="favourites">Favourite</favourite-film-list> -->

      <!-- <component v-bind:is="component"></component>
      <button v-on:click="component = 'favourite-film-list'" :favourites='favourites'>Favourites</button>
      <button v-on:click="component = 'film-list'" :films='films'>List</button> -->

      <!-- <favourite-film-list :favourites="favourites"></favourite-film-list>
      <button v-on:click="favourites">Favourites</button> -->
      <!-- <button v-on:click="hideFilmInfo">Unselect Film</button> -->
      <h1>The Films of Studio Ghibli</h1>
      <img src="https://thumbs.gfycat.com/ShadowyBetterJoey.webp">
      <film-filter-form :films="films" />
    </header>
    <div id="filmDetailWrapper">
    <film-detail :film="selectedFilm"></film-detail>
    </div>
    <div id="filmListWrapper">
    <film-list :films="films"></film-list>
    </div>
    <footer>
      <p>Visit The Official Studio Ghibli website</p>
      <p>Copyright 2019 Davide Campagna</p>
    </footer>
  </div>
</template>

<script>
import FilmFilterForm from './components/FilmFilterForm.vue'
import { eventBus } from './main.js'
import FilmList from './components/FilmList.vue'
import FilmDetail from './components/FilmDetail.vue'
import FavouriteFilmList from './components/FavouriteFilmList.vue'
export default {
  name: "app",
  components: {
    "film-filter-form": FilmFilterForm,
    "film-list": FilmList,
    "film-detail": FilmDetail,
    "favourite-film-list": FavouriteFilmList
  },
  data() {
    return {
      films: [],
      selectedFilm: null,
      favourites: [],
      watched: [],
      watchlist: [],
      watchAgain: []
      // component: "favourite-film-list"
      // websiteTag: '<a href="https://www.studioghibli.com.au/"></a>'
    }
  },
  methods: {
    displayFilmInfo: function(film) {
      this.selectedFilm = film
      },
    markFavourite: function(film) {
      this.favourites.push(film)
      },
    unmarkFavourite: function(film) {
      const index = this.favourites.indexOf(film);
      this.favourites.splice(index, 1)
      },
    isFilmAFavourite: function(film){
      const idsOfFavourites = (this.favourites.map(favourite => favourite.id))
      return idsOfFavourites.includes(film.id)
      },
    markWatched: function(film) {
      this.watched.push(film)
      },
    hasFilmBeenWatched: function(film) {
      const idsOfWatched = (this.watched.map(watched => watched.id))
      return idsOfWatched.includes(film.id)
    },
    markWatchlistItem: function(film) {
      this.watchlist.push(film)
    },
    unmarkWatchlistItem: function(film) {
      const index = this.watchlist.indexOf(film);
      this.watchlist.splice(index, 1)
    },
    isFilmAWatchlistItem: function(film){
      const idsOfWatchlistItems = (this.watchlist.map(watchlist => watchlist.id))
      return idsOfWatchlistItems.includes(film.id)
    },
    hideFilmInfo: function(film){
      this.selectedFilm = null
    },
    markWatchAgainItem: function(film){
      this.hasFilmBeenWatched(film) 
      this.watchAgain.push(film)
    }
  },
  mounted(){
  fetch('https://ghibliapi.herokuapp.com/films')
  .then(res => res.json())
  .then(films => this.films = films)
  eventBus.$on("film-selected", film => this.displayFilmInfo(film));
  eventBus.$on("favourite-added", film => this.markFavourite(film));
  eventBus.$on("favourite-removed", film => this.unmarkFavourite(film));
  eventBus.$on("film-watched", film => this.markWatched(film));
  eventBus.$on("watchlist-added", film => this.markWatchlistItem(film));
  eventBus.$on("watchlist-removed", film => this.unmarkWatchlistItem(film));
  eventBus.$on("film-unselected", film => this.hideFilmInfo(film));
  eventBus.$on("watchAgain-added", film => this.markWatchAgainItem(film));
  }
}
</script>

<style lang="css" scoped>
#app{
  background-image: url('https://i.pinimg.com/originals/5b/39/7b/5b397b87527b8d4d1e299ebfa0f2e9a2.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}

#filmDetailWrapper{
  padding-left: 20;
}

h1{
  color: darkblue;
  font-family: cursive;
  font-size: 4em;
  text-align: center;
}

header{
  /* background-image: url('http://giphygifs.s3.amazonaws.com/media/MEVq1F4Nnsm76/giphy.gif'); */
  text-align: center;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  padding: 20px;
}

footer{
  padding: 6px;
  background-color: lightgrey;
  text-align: center;
  font-size: 10px;
}
</style>
