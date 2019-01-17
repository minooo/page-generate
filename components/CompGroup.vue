<template>
  <div class="mb20">
    <div class="lh150 f14 bold">{{ title }}</div>
    <draggable :options="dragOptions" v-model="list" class="grid">
      <comp-group-list
        v-for="(item, index) in list"
        :key="index"
        :title="item.title"
        :ico="item.ico"
        :comp="item.comp"
      ></comp-group-list>
    </draggable>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import CompGroupList from '~/components/CompGroupList.vue'

export default {
  components: {
    CompGroupList,
    draggable
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
      dragOptions: {
        group: {
          pull: 'clone',
          put: false
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
  grid-auto-rows: 70px;
}
</style>
