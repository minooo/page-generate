<template v-for="(item, index) in list">
  <component :is="item.comp.name" :key="index" v-bind="item.comp.prop">
    <live-show-list v-for="(x, y) in item.children" :key="y" :list="x" />
  </component>
</template>

<script>
import LiveShowList from '~/components/LiveShowList.vue'

export default {
  components: {
    LiveShowList
  },
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
