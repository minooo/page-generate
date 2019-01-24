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
              comp: [
                {
                  name: 'FormItem',
                  tag: 'f-input',
                  prop: {
                    label: 'Input'
                  },
                  comp: [
                    {
                      name: 'Input',
                      prop: {
                        placeholder: 'enter sth1'
                      }
                    }
                  ]
                }
              ]
            },
            {
              title: '多选框',
              ico: 'cube',
              comp: [
                {
                  name: 'FormItem',
                  tag: 'f-checkbox',
                  prop: {
                    label: 'Checkbox'
                  },
                  comp: [
                    {
                      name: 'CheckboxGroup',
                      comp: [
                        { name: 'Checkbox', prop: { label: 'Eat' } },
                        { name: 'Checkbox', prop: { label: 'Sleep' } },
                        { name: 'Checkbox', prop: { label: 'Run' } },
                        { name: 'Checkbox', prop: { label: 'Movie' } }
                      ]
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
</script>
