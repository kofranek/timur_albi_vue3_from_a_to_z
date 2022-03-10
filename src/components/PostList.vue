<template>
  <div v-if="posts_props.length>0">
    <h4>Seznam položek</h4>
    <post-item
        v-for="post in posts_props"
        :post_props="post"
        :key="post.id"
        @deletePost="$emit('clrPost', post)"
    />
  </div>
  <h4 v-else style="color: red">Nejsou žádné položky</h4>
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