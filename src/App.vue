<template lang="html">
  <div>
    <h1>Studio Ghibli Films</h1>
    <film-list :films="films"></film-list>
  </div>
</template>

<script>
import FilmList from './components/FilmList.vue'

export default {
  name: "app",
  components: {
    "film-list": FilmList
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

  }
}
</script>

<style lang="css" scoped>
</style>
