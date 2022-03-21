<template>
  <select
      style="cursor: pointer"
      v-model="modelValue"
      @change="changeOption">
    <option disabled value="">Zvolte ze seznamu</option>
    <option
        v-for="opt in options"
        :key="opt.value"
        :value="opt.value"
    >
      {{ opt.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "MySelect",
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>

</style>