<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h2>Welcome to InstaFeed App</h2>
    <insta />
  </div>
</template>

<script>
import Insta from './components/Insta';

export default {
  name: 'app',
  components: { Insta },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
