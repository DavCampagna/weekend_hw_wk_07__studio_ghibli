<template lang="html">
  <div id="film-list">
    <ul>
      <film-item v-for="film in films"
      :film="film"
      :key="film.id"
      :isFavourite="$parent.isFilmAFavourite(film)">
      </film-item>
    </ul>
  </div>
</template>

<script>
import FilmItem from '@/components/FilmItem.vue'
export default {
  name: "film-list",
  props: ["films"],
  components: {
    "film-item": FilmItem
  },
  methods: {
    deleteFilm: function() {
      this.films.pop()
    }
  }
}
</script>

<style lang="css" scoped>
#film-list{
  width: 100%;
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 20px;
  box-sizing: border-box;
}

/* ul{
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  padding: 0;
}

li{
  flex-grow: 1;
  flex-basis: 300px;
  text-align: center;
  padding: 30px;
  border: 1px solid #222;
  margin: 10px;
} */

</style>
