<template lang="html">
  <div id="app">
    <header>
      <h1>The Films of Studio Ghibli</h1>
      <film-filter-form :films="films" />
    </header>
    <film-detail :film="selectedFilm"></film-detail>
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
      watched: []
      // websiteTag: '<a href="https://www.studioghibli.com.au/"></a>'
    }
  },
  methods: {
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
    }
  },
  mounted(){
  fetch('https://ghibliapi.herokuapp.com/films')
  .then(res => res.json())
  .then(films => this.films = films)
  eventBus.$on('film-selected', film => (this.selectedFilm = film));
  eventBus.$on("favourite-added", film => this.markFavourite(film));
  eventBus.$on("favourite-removed", film => this.unmarkFavourite(film));
  eventBus.$on("film-watched", film => this.markWatched(film));
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

h1{
  color: darkblue;
  font-family: cursive;
  font-size: 4em;
  text-align: center;
}

header{
  /* background-image: url('http://giphygifs.s3.amazonaws.com/media/MEVq1F4Nnsm76/giphy.gif'); */
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}

footer{
  padding: 6px;
  background-color: lightgrey;
  text-align: center;
  font-size: 10px;
}
</style>
