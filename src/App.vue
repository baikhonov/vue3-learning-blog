<template>
  <div class="app">
    <h1>Главная страница</h1>
    <my-input
        v-model="searchQuery"
        placeholder="Поиск..."
    >Поиск
    </my-input>
    <div class="app__btns">
      <my-button
          @click="showDialog"
      >
        Добавить пост
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      ></my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @createPost="createPostHandler"
      />
    </my-dialog>
    <post-list
        v-if="!isPostsLoading"
        :posts="sortedAndSearchedPosts"
        @deletePost="deletePost"
    />
    <div v-else>
      <span class="loader"></span>
    </div>
    <pagination
        :page="page"
        :totalPages="totalPages"
        @changePage="changePage"
    ></pagination>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import Pagination from "@/components/Pagination";
import axios from 'axios';

export default {
  components: {
    PostForm, PostList, Pagination
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По содержимому'}
      ]
    }
  },
  methods: {
    createPostHandler(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    deletePost(post) {
      this.posts = this.posts.filter(item => item.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit,
          }
        });
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
        this.posts = response.data;
      } catch (e) {
        console.log('Ошибка - ', e);
      } finally {
        this.isPostsLoading = false;
      }
    },
    changePage(pageNumber) {
      this.page = pageNumber;
    }
  },
  mounted() {
    this.fetchPosts();

  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    page() {
      this.fetchPosts();
    }
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

.loader {
  width: 48px;
  height: 48px;
  border: 5px solid teal;
  border-bottom-color: transparent;
  border-radius: 50%;
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.app__btns {
  display: flex;
  justify-content: space-between;
  align-items: stretch;

  margin: 15px 0;
}


</style>