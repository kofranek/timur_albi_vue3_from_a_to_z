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

    />
    <div v-if="isPostsLoading">Běží načítání dat</div>
    <div ref="observer" class="observer"></div>
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
      page: 1,
      limit: 10,
      totalPages: 0,
      canLoadPosts: true,
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
        //console.log('fetchPosts: this.isPostsLoading = true')
        setTimeout(async () => {
          //const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          const response = await axios
              .get('https://jsonplaceholder.typicode.com/posts', {
                params: {
                  _page: this.page,
                  _limit: this.limit,
                }
              })
          //console.log('total posts', response.headers['x-total-count'])
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
          //console.log('totalPages', this.totalPages)
          this.posts = response.data
          this.isPostsLoading = false
          console.log('fetchPosts: timeout isPostsLoading', this.isPostsLoading)
          this.page++
          console.log('fetchPost - timeout, page increased to ', this.page)

        }, 1000)
      } catch (e) {
        alert('chyba čtení')
      } finally {
        //this.isPostsLoading = false //ERROR if we use setTime
        //console.log('ERROR: this.isPostsLoading = false ERROR if we use setTime')
      }
    },
    async loadMorePosts() {
      console.log('***loadMorePosts***')
      try {
        this.isPostsLoading = true
        setTimeout(async () => {
          //const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
          const response = await axios
              .get('https://jsonplaceholder.typicode.com/posts', {
                params: {
                  _page: this.page,
                  _limit: this.limit,
                }
              })
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
          console.log('**from setTimeout ** this.totalPages=', this.totalPages)
          this.posts = [...this.posts, ...response.data]
          this.isPostsLoading = false
          this.page++
          this.canLoadPosts = true
        }, 5000)
      } catch (e) {
        alert('chyba čtení')
      } finally {
        console.log('finally (before setTimeout ended!')
      }
    },
  },
  mounted() {
    const options = {
      rootMargin: '0px',
      threshold: 1.0
    }
    const callback = (entries, options) => {
      console.log('Překřížení')
      console.log('entries=', entries)
      if (entries[0].isIntersecting) {
        console.log('totalPages=', this.totalPages)
        console.log('jdu dovnitř page=', this.page)
        if (this.totalPages === 0 || this.page <= this.totalPages) {
          if (this.canLoadPosts) {
            this.loadMorePosts()
            console.log('*** loudím posty ze stránky =', this.page, '*****')
            this.canLoadPosts = false
          }

        }
      } else {
        console.log('jdu ven')
      }
    }
    const observer = new IntersectionObserver(callback, options);
    console.log('this.$refs.observer=', this.$refs.observer)
    observer.observe(this.$refs.observer)
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) =>
          post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts() {
      //console.log('this.searchQuery', this.searchQuery)
      return this.sortedPosts
          .filter(post =>
              post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    // page() {
    //   //page(newValue){
    //   //console.log('page=',newValue)
    //   //zavolá se když se změní stránky (nemusíme vypisovat hodnotu)
    //   this.fetchPosts()
    // },
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

.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
}

.current-page {
  border: 2px solid teal;
}

.observer {
  height: 30px;
  background: green;

}
</style>
