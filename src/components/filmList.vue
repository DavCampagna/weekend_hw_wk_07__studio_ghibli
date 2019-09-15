<template lang="html">
  <div id="film-list">
    <ul>
      <film-item v-for="film in films"
      :film="film"
      :key="film.id"
      :isFavourite="$parent.isFilmAFavourite(film)"
      :hasBeenWatched="$parent.hasFilmBeenWatched(film)"
      :isWatchlistItem="$parent.isFilmAWatchlistItem(film)">
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

</style>
