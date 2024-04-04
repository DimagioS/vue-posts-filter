<template>
  <div class="container">
    <div class="grid-container">
      <div v-for="post in posts" :key="post.id">
        <PostItem :post="post" />
      </div>
    </div>
    <div class="text-center" v-if="!posts.length">
      No posts found.
    </div>
  </div>
</template>

<script>
import PostItem from './PostItem.vue';

export default {
  components: {
    PostItem
  },

  props: {
    posts: {
      type: Array,
      required: true
    }
  },
}
</script>

<style lang="scss" src="../styles/postsList.scss" scoped></style>