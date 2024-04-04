<template>
  <AuthorFilter v-model="searchQuery" />
  <LoaderItem v-if="loadingPost" />
  <PostsList v-else :posts="filteredPosts" />
</template>

<script>
import debounce from 'lodash.debounce';
import PostsList from './components/PostsList.vue';
import AuthorFilter from './components/AuthorFilter.vue';
import LoaderItem from './components/Loader.vue';
import { $api } from './services/apiService';

export default {
  components: { 
    PostsList,
    AuthorFilter,
    LoaderItem
  },

  data() {
    return {
      posts: [],
      filteredPosts: [],
      searchQuery: '',
      loadingPost: false,
    }
  },

  methods: {
    async fetchPosts() {
      try {
        this.loadingPost = true;
        const response = await $api.get('/posts', {
          params: {
            _expand: 'user',
          },
        });

        if (!response.data) {
          throw new Error('Failed to retrieve data. Please try refreshing the page.');
        }

        this.posts = response.data;
        this.filterPosts();
      } catch (error) {
        console.error(error);
      } finally {
        this.loadingPost = false;
      }
    },

    filterPosts() {
      this.filteredPosts = this.posts.filter((post) => post?.user?.name.toLocaleLowerCase().includes(this.searchQuery.toLocaleLowerCase()))
    },
  },

  watch: {
    searchQuery() {
      this.debouncedFilterPosts();
    }
  },

  created() {
    this.debouncedFilterPosts = debounce(this.filterPosts, 300);
  },

  mounted() {
    this.fetchPosts();
  }
}
</script>

<style></style>
