<template lang="html">
  <!-- <form v-on:submit.prevent>
    <label>🔎 </label>
    <input type="text" v-model="search" placeholder="search for a film..." v-on:keyup="searchForFilm">
    <select v-on:change="handleSelect" v-model="selectedFilm">
      <option disabled value="">Select a film...</option>
      <option v-for="film in films" :value="film">{{film.title}}</option>
    </select>
  </form> -->
  <form v-on:submit.prevent>
  <p> Search for a Studio Ghibli Film </p>
  <input list="films_search" v-model="search" v-on:keyup.enter="searchForFilm">
  <datalist id="films_search" v-on:change="handleSelect" v-model="selectedFilm">
    <option v-for="film in films" :film="film">{{film.title}}</option>
  </datalist>
  <div></div>
  <input type="image" id="magnifying_glass" src="https://loading.io/spinners/magnify/index.searching-for-loading-icon.svg" v-on:click="searchForFilm">
</form>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "film-filter-form",
  data(){
    return {
      "search": "",
      "selectedFilm": {},
    }
  },
  props: ["films"],
  methods: {
    searchForFilm(){
      let foundFilm = this.films.find((film) => {
        return film.title.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedFilm = foundFilm

      eventBus.$emit('film-selected', this.selectedFilm)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('film-selected', this.selectedFilm)
    }
  }
}
</script>

<style lang="css" scoped>

p{
  font-size: 25px;
  color: rgb(255, 77, 77);
  font-family: cursive;
  text-align: center;
}

form{
  text-align: center;
  margin: 40px 0;
}

input{
  width: 25%;
}

#magnifying_glass{
  width: 50px;
}
/* select, input[type="text"]{
  font-size: 18px;
}

select {
  margin-left: 20px;
} */
</style>
