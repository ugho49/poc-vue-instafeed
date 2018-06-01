<template>
  <vue-instagram token="accessTokenHere" username="kevinongko" :count="5">
    <template slot="feeds" slot-scope="props">
      <li class="fancy-list"> {{ props.feed.link }} </li>
    </template>
    <template slot="error" slot-scope="props">
      <div class="fancy-alert"> {{ props.error.error_message }} </div>
    </template>
  </vue-instagram>
</template>

<script>
import VueInstagram from 'vue-instagram';

export default {
  name: 'InstaFeed',
  components: { VueInstagram },
  data() {
    return {
      accessTokenHere: '',
      username: 'ugho49',
    };
  },
  created() {
  },
};
</script>
