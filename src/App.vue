<template>
  <div id="app">
    <HomePage />
  </div>
</template>

<script>
import HomePage from '@/components/HomePage.vue';

export default {
  components: {
    HomePage,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #fff;
}
</style>
