<template>
  <div class="insta-post">
    <img :src="img" alt="Image Instagram" @load="imgLoaded = true">
    <div v-if="imgLoaded" class="timeago">{{ timeago }}</div>
  </div>
</template>

<script>
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
    timeago() {
      return '7 min ago';
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
    right: 0px;
    padding: 10px;
  }
}
</style>
