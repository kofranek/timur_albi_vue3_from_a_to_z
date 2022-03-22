<template>
  <div v-if="posts_props.length>0">
    <h4>Seznam položek</h4>
    <transition-group name="list">
      <post-item
          v-for="post in posts_props"
          :post_props="post"
          :key="post.id"
          @deletePost="$emit('clrPost', post)"
      />
    </transition-group>

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
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
  position: absolute;
}
</style>