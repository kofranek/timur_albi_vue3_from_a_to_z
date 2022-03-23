<template>
  <div class="app">
    <h1>Dialog s položkami</h1>
    <my-input
        type="text"
        v-model="searchQuery"
        placeholder="Název hledané položky..."
    />
    <div class="app__btns">
      <my-button
          @click="showDialog"

      >
        vytvořit položku
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>
<!--    <post-list-->
<!--        :posts_props="sortedPosts"-->
<!--        @clrPost="deletePost"-->
<!--        v-if="!isPostsLoading"-->
<!--    />-->
    <post-list
        :posts_props="sortedAndSearchedPosts"
        @clrPost="deletePost"
        v-if="!isPostsLoading"
    />
    <div v-else>Běží načítání dat</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios'

export default {
  components: {
    PostForm: PostForm,
    PostList: PostList
  },
  name: "App",
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      sortOptions: [
        {value: 'title', name: 'Podle názvu'},
        {value: 'body', name: 'Podle obsahu'}
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false
    },
    deletePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        setTimeout(async () => {
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          this.posts = response.data
        }, 1000)
      } catch (e) {
        alert('chyba čtení')
      } finally {
        this.isPostsLoading = false
      }
    },
  },
  mounted() {
    //console.log('mounted')
    this.fetchPosts()
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) =>
          post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      console.log('this.searchQuery', this.searchQuery)
       return this.sortedPosts
           .filter(post =>
               post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },

  watch: {
    selectedSort(newValue) {  //když se mění hodnpta
      console.log(newValue)
    //   this.posts.sort((post1, post2) => {
    //     // return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
    //     return post1[newValue]?.localeCompare(post2[newValue])
    //   })
    },
    dialogVisible(newValue) {
      console.log(newValue)
    }
  }
}



</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app__btns {
  display: flex;
  justify-content: space-between;
  margin: 15px 0;
}

</style>
