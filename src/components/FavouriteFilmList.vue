<template lang="html">
  <div>
    <ul>
      <favourite-film-item
        v-for="film in favourites"
        :film="film"
        :key="film.id"
      ></favourite-film-item>
    </ul>
  </div>
</template>

<script>
import FavouriteFilmItem from "@/components/FavouriteFilmItem";

export default {
  name: "favourite-film-list",
  props: ["favourites"],
  components: {
    "favourite-film-item": FavouriteFilmItem
  }
};
</script>

<style lang="css" scoped>
</style>
