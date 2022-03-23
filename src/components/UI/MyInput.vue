<template>
  <input
      class='input'
      type="text"
      :modelValue="value"
      @input="updateInput"
  >
</template>

<script>
export default {
  name: "MyInput",
  props: {
    value: [String, Number]
  },
  methods: {
    updateInput(event) {
      //console.log(event.target.value)
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>