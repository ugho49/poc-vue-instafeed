<template>
  <div class="insta-feed">
    <insta-post v-for="(post, index) of posts" :key="index" :post="post"/>
  </div>
</template>

<script>
import axios from 'axios';
import InstaPost from './insta-post';

const LS_INSTA_POSTS = 'LS_INSTA_POSTS';
const LS_INSTA_LAST_UPDATE_TIME = 'LS_INSTA_LAST_UPDATE_TIME';
const INSTA_USER_ID = '178738305';
const INSTA_ACCESS_TOKEN = '178738305.1677ed0.7b695f0d8f9c478293d7cf25587583e8';
const UPDATE_INSTA_SECOND_TIME = 45; // Every 45 seconds

export default {
  name: 'InstaFeed',
  components: { InstaPost },
  data() {
    return {
      posts: [],
      getPostInterval: null,
    };
  },
  mounted() {
    this.getPosts();
    this.getPostInterval = setInterval(() => {
      this.getPosts();
    }, 5000);
  },
  beforeDestroy() {
    if (this.getPostInterval) {
      clearInterval(this.getPostInterval);
    }
  },
  methods: {
    getPosts() {
      const lastUpdateTime = localStorage.getItem(LS_INSTA_LAST_UPDATE_TIME) || null;

      if (lastUpdateTime === null || this.canRequest(lastUpdateTime)) {
        // Get from API
        this.getPostsFromApi();
      } else {
        // Get from LocalStorage
        this.getPostsFromLocalStorage();
      }
    },
    canRequest(lastUpdateTime) {
      const now = new Date();
      const storageDate = new Date(lastUpdateTime);
      const dif = now.getTime() - storageDate.getTime();
      const secondsBetweenDates = Math.trunc(dif / 1000);
      return secondsBetweenDates >= UPDATE_INSTA_SECOND_TIME;
    },
    getPostsFromLocalStorage() {
      this.posts = JSON.parse(localStorage.getItem(LS_INSTA_POSTS)) || [];
    },
    getPostsFromApi() {
      axios.get(`https://api.instagram.com/v1/users/${INSTA_USER_ID}/media/recent?access_token=${INSTA_ACCESS_TOKEN}`)
        .then((res) => {
          this.posts = res.data.data;
          localStorage.setItem(LS_INSTA_POSTS, JSON.stringify(this.posts));
        }).catch((err) => {
          console.error(err);
          if (this.posts.length === 0) {
            this.getPostsFromLocalStorage();
          }
        });
      localStorage.setItem(LS_INSTA_LAST_UPDATE_TIME, new Date());
    },
  },
};
</script>

<style lang="scss" scoped>
.insta-feed {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
