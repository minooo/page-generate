<template>
  <draggable @start="onDragStart" @end="onDragEnd">
    <div class="flex fd-c ai-c w-100 move">
      <i :class="`ivu-icon ivu-icon-md-${ico} f36`"></i>
      <span>{{ text }}</span>
    </div>
  </draggable>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  components: {
    draggable
  },
  props: {
    // 检测类型 + 其他验证
    text: {
      type: String,
      default: '组件名字',
      required: true,
      validator: function(value) {
        return value && value.length <= 8
      }
    },
    ico: {
      type: String,
      default: 'cube',
      required: true
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
  },
  methods: {
    onDragStart: function(e) {
      console.log('start', e)
    },
    onDragEnd: function(e) {
      console.log('end', e)
    }
  }
}
</script>

<style>
</style>
