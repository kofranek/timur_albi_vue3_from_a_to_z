<template>
  <div>
    <button v-on:click="addLike">like</button>
    <button v-on:click="addDislike">dislike</button>
  </div>
  <div>
    <div>likes count: <strong> {{ likes }}</strong></div>
    <div>dislikes count: <strong> {{ dislikes }}</strong></div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      likes: 0,
      dislikes: 0,
    }
  },
  methods: {
    addLike() {
      this.likes++
    },
    addDislike() {
      this.dislikes++
    },
  },
}
</script>

<style scoped>

</style>