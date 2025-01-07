<template>
  <div v-if="posts.length > 0" class="posts">
    <h2>Список постов</h2>
    <transition-group name="post-list">
      <post-item
          v-for="post in posts"
          :key="post.id"
          :post="post"
          @deletePost="$emit('deletePost', post)"
      />
    </transition-group>

  </div>
  <h2 v-else class="posts__empty">Нет постов</h2>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.posts__empty {
  color: red;
}
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
  transition: transform 0.4s ease;
}
</style>