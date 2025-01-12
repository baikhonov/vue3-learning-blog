<template>

  <navbar></navbar>
  <div class="app">
    <router-view></router-view>

  </div>
</template>

<script>
import Navbar from "@/components/Navbar";
export default {
  components: {
    Navbar
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  overflow-x: hidden;
}

.app {
  padding: 20px;
}
</style>