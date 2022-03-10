<template>
  <div class="app">
    <h1>Dialog s položkami</h1>
    <my-button
        @click="showDialog"
        style="margin:15px 0;"
    >Vytvořit položku
    </my-button>
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

export default {
  components: {
    PostForm: PostForm,
    PostList: PostList
  },
  name: "App",
  data() {
    return {
      posts: [
        {id: 1, title: 'Hlavička dopisu 1', body: 'Obsah dopisu 1'},
        {id: 2, title: 'Hlavička dopisu 2', body: 'Obsah dopisu 2'},
        {id: 3, title: 'Hlavička dopisu 3', body: 'Obsah dopisu 3'},
        {id: 4, title: 'Hlavička dopisu 4', body: 'Obsah dopisu 4'},
      ],
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