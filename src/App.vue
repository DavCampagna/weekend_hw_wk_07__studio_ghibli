<template lang="html">
  <div>
    <header>
      <h1>Studio Ghibli Films</h1>
    </header>
    <film-filter-form :film="film" />
    <film-list :films="films"></film-list>
    <film-detail :film="selectedFilm"></film-detail>
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
      selectedFilm: null
      // websiteTag: '<a href="https://www.studioghibli.com.au/"></a>'
    }
  },
  methods: {
  },
  mounted(){
  fetch('https://ghibliapi.herokuapp.com/films')
  .then(res => res.json())
  .then(films => this.films = films)
  eventBus.$on('film-selected', (film) => {
    this.selectedFilm = film
    })
  }
}
</script>

<style lang="css" scoped>
h1{
  color: purple;
  font-family: cursive;
  text-align: center;
}

header{
  background-color: lightyellow;
  padding: 10px;
}

footer{
  padding: 6px;
  background-color: lightgrey;
  text-align: center;
  font-size: 10px;
}
</style>
