<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title text-primary">{{ post.title }}</h5>
      <p class="card-text">{{ post.body }}</p>
      <span class="card-user-info">{{ post.user.name }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" src="../styles/postItem.scss" scoped></style>