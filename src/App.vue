<template>
  <MakeTag />
</template>

<script>
import MakeTag from "./components/MakeTag.vue";

export default {
  name: 'App',
  components: {
    MakeTag
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  background: rgb(29, 29, 29);
}
</style>
