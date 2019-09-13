<template lang="html">
  <div>
      <p>{{film.title}}</p>
  </div>
</template>

<script>
export default {
  name: "film-item",
  props: ["film"]
}
</script>

<style lang="css" scoped>
</style>
