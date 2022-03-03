<template>
  <form @submit.prevent>
    <h4>Vytvoření položky</h4>
    <input class="input"
           type="text"
           placeholder="Název"
           v-bind:value="post.title"
           @input="post.title = $event.target.value"
    >
    <input class="input"
           type="text"
           placeholder="Obsah"
           v-bind:value="post.body"
           @input="post.body = $event.target.value"
    >
    <button class="btn"
    >
      Vytvořit položku
    </button>
  </form>

</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  }
}

</script>

<style scoped>
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