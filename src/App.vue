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
  margin: auto;
  max-width: 900px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
