<template>
  <div id="app">
    <Pokemon /> <!-- on appelle le component pokemon -->
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'
export default {
  components: {
    Pokemon
  }
}
</script>

<style lang="scss"> // Le CSS
  @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');

  body {
    margin: 0;
    padding: 0;
    background: rgb(46, 46, 46);
  }
</style>