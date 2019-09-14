<template lang="html">
  <article v-if="film" id="filmDetail">
    <h1>Film Info</h1>
    <p>{{film.title}}</p>
    <p>{{film.director}}</p>
    <p>{{film.release_date}}</p>
    <p>{{film.description}}</p>
  </article>
</template>

<script>
export default {
  name: "film-detail",
  props: ["film"]
}
</script>

<style lang="css" scoped>
#filmDetail {

}

h1{
  color: purple;
  font-family: cursive;
  text-align: center;
}

p{
  color: black;
  text-align: center;
}

</style>
