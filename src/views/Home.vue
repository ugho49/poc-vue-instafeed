<template>
  <div class="home">
    <img src="../assets/logo.png">
    <InstaFeed />
  </div>
</template>

<script>
import InstaFeed from '../components/insta-feed';

export default {
  name: 'home',
  components: {
    InstaFeed,
  },
};
</script>
