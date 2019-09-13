<template lang="html">
  <div>
    <ul>
      <film-item v-for="film in films" :film="film" :key="index"></film-item>
    </ul>
  </div>
</template>

<script>
import filmItem from '@/components/filmItem.vue'

export default {
  name: "film-list",
  props: ["films"],
  components: {
    "film-item": filmItem
  }
}
</script>

<style lang="css" scoped>
</style>
