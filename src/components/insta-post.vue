<template>
  <div class="insta-post">
    <img :src="img" alt="Image Instagram" @load="imgLoaded = true">
    <div v-if="imgLoaded" class="timeago">{{ timeago }}</div>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'InstaPost',
  props: {
    post: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      imgLoaded: false,
    };
  },
  computed: {
    img() {
      return this.post.images.low_resolution.url;
    },
    createdAt() {
      return new Date(this.post.created_time * 1000);
    },
    timeago() {
      return moment(this.createdAt).fromNow();
    },
  },
};
</script>

<style lang="scss" scoped>
.insta-post {
  width: fit-content;
  margin: 10px;
  position: relative;

  .timeago {
    background: rgba(128, 128, 128, 0.75);
    color: #ffffff;
    width: 120px;
    font-weight: 600;
    position: absolute;
    bottom: 4px;
    right: 0;
    padding: 10px;
    visibility: hidden;
    opacity: 0;
    transition: visibility 0.2s, opacity 0.2s linear;
  }

  &:hover {
    .timeago {
      visibility: visible;
      opacity: 1;
    }
  }
}
</style>
