<template lang="html">
  <article v-if="film" id="filmDetail">
    <h1>Film Info</h1>
    <h2>{{film.title}}</h2>
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
  font-size: 2em;
  font-family: cursive;
  text-align: center;
}

h2{
  font-size: 3em;
  color: crimson;
  font-family: cursive;
  text-align: center;
}

p{
  color: black;
  text-align: center;
}

</style>
