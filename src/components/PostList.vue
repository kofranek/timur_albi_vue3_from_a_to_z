<template>
  <div >
    <h4>Seznam položek</h4>
    <post-item
        v-for="post in posts_props"
        :post_props="post"
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
}
</script>

<style scoped>


</style>