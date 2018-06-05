<template>
  <div id="app">
    <img src="./assets/logo.png">
    <insta-feed />
  </div>
</template>

<script>
import moment from 'moment';
import InstaFeed from './components/insta-feed';

export default {
  name: 'app',
  components: { InstaFeed },
  created() {
    moment.locale('fr');
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
  margin-top: 60px;
}
</style>
