<template>
  <div>123</div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      dragOptions: {
        group: {
          put: true
        },
        animation: 300
      }
    }
  }
}
</script>

<style scoped>
</style>
