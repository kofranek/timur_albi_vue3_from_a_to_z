<template>
  <div class="post" v-for="post in posts_props">
    <div><strong>{{ post.title }}</strong> {{ post.body }}</div>
  </div>
</template>

<script>
export default {
  name: "PostList",
  props: {
    posts_props: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

</style>