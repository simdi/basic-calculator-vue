<template>
  <div id="app">
    <HomePage/>
  </div>
</template>

<script>
import HomePage from './components/HomePage.vue';

export default {
  name: 'app',
  components: {
    HomePage,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 100px auto;
  display: flex;
  justify-content: center;
}
.header {
  height: 50px;
  width: 100%;
}
.content {
  width: 100%;
}
</style>
