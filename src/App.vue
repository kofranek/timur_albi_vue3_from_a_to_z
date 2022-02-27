<template>
  <div class="post" v-for="post in posts" >
    <div><strong>{{post.title}}</strong> {{post.body}}</div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      posts:[
        {id: 1, title: 'Hlavička dopisu 1', body: 'Obsah dopisu 1'},
        {id: 2, title: 'Hlavička dopisu 2', body: 'Obsah dopisu 2'},
        {id: 3, title: 'Hlavička dopisu 3', body: 'Obsah dopisu 3'},
        {id: 4, title: 'Hlavička dopisu 4', body: 'Obsah dopisu 4'},
      ]
    }
  },
  methods: {},
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

</style>