<template>
  <div>
    <div class="lh150 f14 bold">{{ title }}</div>
    <div class="grid mb20">
      <comp-group-list v-for="(item, index) in list" :key="index" :text="item.text" :ico="item.ico"></comp-group-list>
    </div>
  </div>
</template>

<script>
import CompGroupList from '~/components/CompGroupList.vue'

export default {
  components: {
    CompGroupList
  },
  props: {
    // 检测类型 + 其他验证
    title: {
      type: String,
      default: '标题',
      required: true,
      validator: function(value) {
        return value && value.length <= 8
      }
    },
    list: {
      type: Array,
      required: true,
      validator: function(value) {
        return value && value.length > 0
      }
    }
  },
  data() {
    return {
      value: '',
      single: false,
      fromOptions: {
        group: {
          name: 'components',
          pull: 'clone' // To clone: set pull to 'clone'
        }
      }
    }
  }
}
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-auto-rows: 60px;
}
</style>
