<template>
  <div class="flex fd-c jc-c ai-c h-100 move">
    <i :class="`ivu-icon ivu-icon-md-${ico} f30 mb5`"/>
    <span>{{ title }}</span>
  </div>
</template>

<script>
export default {
  props: {
    // 检测类型 + 其他验证
    title: {
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
    },
    comp: {
      type: Array,
      required: true
    }
  }
}
</script>

<style>
</style>
