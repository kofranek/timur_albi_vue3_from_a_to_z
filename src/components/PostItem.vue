<template>
  <div class="post">
    <div>
      <div><strong>Název: </strong>{{ post_props.title }}</div>
      <div><strong>Obsah: </strong>{{ post_props.body }}</div>
    </div>
    <div class="post__btns">
      <button class="btn" @click="deletePost">Odstranit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: {
    post_props: {
      type: Object,
      required: true,
    }
  },
  methods: {
    deletePost() {
      console.log('PostItem: post_props=', this.post_props)
      this.$emit('deletePost', this.post_props)
    }
  }
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>