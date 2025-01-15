<template>
  <div class="navbar">
    <div @click="$router.push('/')">Vue 3</div>
    <div class="navbar__btns">
      <my-button @click="$router.push('/posts')">Посты</my-button>
      <my-button @click="$router.push('/about')">О проекте</my-button>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.navbar {
  display: flex;
  align-items: center;
  gap: 10px;

  height: 50px;
  padding: 0 15px;

  background-color: lightgray;
  box-shadow: 2px 2px 4px gray;
}
.navbar__btns {
  display: flex;
  gap: 20px;
  margin-left: auto;
}
</style>