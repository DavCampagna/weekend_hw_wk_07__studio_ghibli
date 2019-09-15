<template lang="html">
  <article>
    <div v-if="film" id="filmDetail">
    <h1>Film Info</h1>
    <h2>{{film.title}}</h2>
    <p>{{film.director}}</p>
    <p>{{film.release_date}}</p>
    <p>{{film.description}}</p>
    </div>
  </div>
  </article>
</template>

<script>
export default {
  name: "film-detail",
  props: ["film"]
}
</script>

<style lang="css" scoped>

article{
  background-color: hsla(60, 92%, 72%, 0.49);
  padding: 0px;
}

h1{
  color: steelblue;
  font-size: 2em;
  font-family: cursive;
  text-align: center;
}

h2{
  font-size: 3em;
  color: rgb(255, 0, 128);
  text-shadow:5px 5px 10px white;
  font-family: cursive;
  text-align: center;
}

p{
  color: black;
  text-align: center;
}

#close_icon{

}

</style>
