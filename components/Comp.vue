<template>
  <div class="o-h r4" style="width: 260px">
    <div class="f18 bold lh150 ptb20 b-b mb20">组件列表区</div>
    <comp-group v-for="(item, index) in compArr" :key="index" :title="item.title" :list="item.list"></comp-group>
  </div>
</template>

<script>
import CompGroup from '~/components/CompGroup.vue'

export default {
  components: {
    CompGroup
  },
  data() {
    return {
      dragOptions: {
        group: {
          put: true
        },
        animation: 300
      },
      compArr: [
        {
          title: '表单',
          list: [
            {
              title: '输入框',
              ico: 'cube',
              comp: {
                name: 'Input',
                prop: {
                  placeholder: 'enter sth1'
                }
              }
            },
            {
              title: '多选框',
              ico: 'cube',
              comp: {
                name: 'Checkbox',
                prop: {
                  placeholder: 'enter sth2'
                }
              }
            }
          ]
        }
      ]
    }
  }
}
</script>
