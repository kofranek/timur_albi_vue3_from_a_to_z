<template>
  <form @submit.prevent>
    <h4>Vytvoření položky</h4>
    <input class="input"
           type="text"
           placeholder="Název"
           v-model="post.title"
    >
    <input class="input"
           type="text"
           placeholder="Obsah"
           v-model="post.body"

    >
    <my-button
        @click="createPost"
        style="align-self: flex-end; margin-top: 15px"
    >
      Vytvořit položku
    </my-button>
  </form>

</template>

<script>
import MyButton from "@/components/UI/MyButton"
export default {
  components: {MyButton},
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      if (this.post.title && this.post.body) {
        this.post.id = Date.now()
        this.$emit('create', this.post)
        this.post = {
          title: '',
          body: ''
        }
      }
    },
  }
}

</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>