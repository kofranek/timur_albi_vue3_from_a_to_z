<template>
  <div>
    <h4>Seznam položek</h4>
    <post-item
        v-for="post in posts_props"
        :post_props="post"
        :key="post.id"
        @deletePost="$emit('clrPost', post)"
    />
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {PostItem},
  props: {
    posts_props: {
      type: Array,
      required: true
    }
  },
  methods: {
    // deletePost(post) {
    //   console.log('PostList:delete:',post)
    //   this.$emit('clrPost', post)
    // },
  }
}
</script>

<style scoped>


</style>