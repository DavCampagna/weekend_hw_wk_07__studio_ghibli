<template lang="html">
  <div>
      <p v-on:click="handleClick">{{film.title}} <button v-on:click="addFavourite">Add to Favourites</button></p>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: "film-item",
  props: ["film"],
  methods: {
  handleClick(){
    eventBus.$emit('film-selected', this.film)
    },
  addFavourite(){
    eventBus.$emit('favourite-added', this.film)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
