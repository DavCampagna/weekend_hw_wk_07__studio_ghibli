<template lang="html">
  <article>
    <div v-if="film">
    <h1>Film Info</h1>
    <h2>{{film.title}}</h2>
    <p>{{film.director}}</p>
    <p>{{film.release_date}}</p>
    <p>{{film.description}}</p>
  </div>

  </article>
</template>

<script>
export default {
  name: "film-detail",
  props: ["film"],
  methods: {
    unselectFilm(){
      eventBus.$emit("film-unselected", this.film)
    }
  }
}
</script>

<style lang="css" scoped>

article{
  background-color: hsla(60, 92%, 72%, 0.49);
  margin: 20px;
  border-radius: 15px;
  /* padding-bottom: 20px; */
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
  line-height: 30px;
}

#close_icon{

}

</style>
