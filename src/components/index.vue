<template>
  <div>
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import { bar } from "@/components/header/bar.vue"
export default {
  name: 'index',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
