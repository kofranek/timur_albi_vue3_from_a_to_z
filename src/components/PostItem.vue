<template>
  <div class="post">
    <strong>{{ post_props.title }}</strong> {{ post_props.body }}
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
  }
}
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}
</style>