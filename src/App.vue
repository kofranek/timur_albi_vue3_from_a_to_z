<template>
  <div class="app">
    <post-form
        @create="createPost"
    />
    <post-list :posts_props="posts" @clrPost="deletePost"/>
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
      // title: '',
      // body: ''
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post)
    },
    deletePost(post) {
      const idx = this.posts.findIndex((el) => {
        return (el.id === post.id)
      })
      this.posts.splice(idx,1)
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