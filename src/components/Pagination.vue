<template>
  <div class="page__wrapper">
    <div
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        class="page"
        :class="{
            'page-current': page === pageNumber
          }"
        @click="$emit('changePage', pageNumber)"
    >
      {{ pageNumber }}
    </div>
  </div>
</template>

<script>
export default {
  name: "pagination",
  props: {
    totalPages: {
      type: Number,
      required: true
    },
    page:  {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.page__wrapper {
  display: flex;
  justify-content: center;
  margin: 15px auto;
  gap: 10px;
}
.page {
  padding: 10px;
  border: 1px solid black;
  cursor: pointer;
}
.page-current {
  border: 2px solid teal;
}
</style>