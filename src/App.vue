<template>
  <div class="app">
    <h1>Dialog s položkami</h1>
    <my-button @click="fetchPosts">
      dostat posty
    </my-button>
    <my-button
        @click="showDialog"
        style="margin:15px 0;"
    >Vytvořit položku
    </my-button>
    <!--    <my-dialog v-model="dialogVisible">-->
    <!--      <post-form-->
    <!--          @create="createPost"-->
    <!--      />-->
    <!--    </my-dialog>-->
    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <post-list
        :posts_props="posts"
        @clrPost="deletePost"
    />
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
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
      this.dialogVisible = false
    },
    deletePost(post) {
      // const idx = this.posts.findIndex((el) => {
      //   return (el.id === post.id)
      // })
      // this.posts.splice(idx,1)
      //***************************************************************
      // místo findIndex a splice použijeme k odstranění položky filter
      //***************************************************************
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    async fetchPosts() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
        console.log(response)
        this.posts = response.data
        console.log(this.posts)
      } catch (e) {
        alert('chyba čtení')
      }
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


</style>