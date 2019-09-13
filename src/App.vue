<template lang="html">
  <div>
    <h1>Studio Ghibli Films</h1>
    <film-list :films="films"></film-list>
    <film-detail :film="selectedFilm"></film-detail>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import FilmList from './components/FilmList.vue'
import FilmDetail from './components/FilmDetail.vue'

export default {
  name: "app",
  components: {
    "film-list": FilmList,
    "film-detail": FilmDetail
  },
  data() {
    return {
      films: [],
      selectedFilm: null
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
</style>
