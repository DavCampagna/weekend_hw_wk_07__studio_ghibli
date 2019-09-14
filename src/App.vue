<template lang="html">
  <div>
    <header>
      <h1>The Films of Studio Ghibli</h1>
      <film-filter-form :films="films" />
    </header>
    <film-detail :film="selectedFilm"></film-detail>
    <film-list :films="films"></film-list>
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
export default {
  name: "app",
  components: {
    "film-filter-form": FilmFilterForm,
    "film-list": FilmList,
    "film-detail": FilmDetail
  },
  data() {
    return {
      films: [],
      selectedFilm: null,
      favourites: []
      // websiteTag: '<a href="https://www.studioghibli.com.au/"></a>'
    }
  },
  methods: {
    markFavourite: function(film) {
    this.favourites.push(film)
    }
  },
  mounted(){
  fetch('https://ghibliapi.herokuapp.com/films')
  .then(res => res.json())
  .then(films => this.films = films)
  eventBus.$on('film-selected', film => (this.selectedFilm = film));
  eventBus.$on("favourite-added", film => this.markFavourite(film));
  }
}
</script>

<style lang="css" scoped>
h1{
  color: darkblue;
  font-family: cursive;
  text-align: center;
}

header{
  background-image: url('https://media.giphy.com/media/Uz4cDaGXPxeuY/giphy.gif');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  height: 50vh;
  padding:50;
  margin:50;
}

footer{
  padding: 6px;
  background-color: lightgrey;
  text-align: center;
  font-size: 10px;
}
</style>
