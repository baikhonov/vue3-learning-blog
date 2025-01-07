<template>
  <form @submit.prevent>
    <h2>Добавление поста</h2>
    <my-input
        placeholder="Название"
        v-model="post.title"
    ></my-input>
    <my-input
        placeholder="Описание"
        v-model="post.body"
    ></my-input>
    <my-button
        style="align-self: flex-end; margin-top: 15px;"
        @click="createPost"
        type="submit"
    >
      Добавить
    </my-button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('createPost', this.post);
      this.post = {
        title: '',
        body: ''
      }
    }
  },
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}



</style>