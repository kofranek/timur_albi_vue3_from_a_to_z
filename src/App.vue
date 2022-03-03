<template>
  <div class="app">
    <form @submit.prevent>
      <h4>Vytvoření položky</h4>
      <!--    <input class="input"-->
      <!--           type="text"-->
      <!--           placeholder="Název"-->
      <!--           v-bind:value="title"-->
      <!--           @input="inputTitle"-->
      <!--    >-->
      <!--    <input class="input"-->
      <!--           type="text"-->
      <!--           placeholder="Obsah"-->
      <!--           v-bind:value="body"-->
      <!--           @input="inputBody"-->
      <!--    >-->

      <input class="input"
             type="text"
             placeholder="Název"
             v-bind:value="title"
             @input="title = $event.target.value"
      >
      <input class="input"
             type="text"
             placeholder="Obsah"
             v-bind:value="body"
             @input="body = $event.target.value"
      >
      <button class="btn"
              @click.prevent="createPost"
      >
        Vytvořit položku
      </button>
    </form>


    <div class="post" v-for="post in posts">
      <div><strong>{{ post.title }}</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      posts: [
        {id: 1, title: 'Hlavička dopisu 1', body: 'Obsah dopisu 1'},
        {id: 2, title: 'Hlavička dopisu 2', body: 'Obsah dopisu 2'},
        {id: 3, title: 'Hlavička dopisu 3', body: 'Obsah dopisu 3'},
        {id: 4, title: 'Hlavička dopisu 4', body: 'Obsah dopisu 4'},
      ],
      title: '',
      body: ''
    }
  },
  methods: {
    // inputTitle(event) {
    //   this.title = event.target.value
    // },
    // inputBody(event) {
    //   this.body = event.target.value
    // }
    createPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body,
      }
      this.posts.push(newPost)
      this.title = ''
      this.body = ''
    },
  },
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

form {
  display: flex;
  flex-direction: column;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

</style>