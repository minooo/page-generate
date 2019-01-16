<template>
  <div>
    <div class="bg-main c-white plr20 ptb15 f18 bold">页面构造器（v0.0.1）</div>
    <div class="flex plr20">
      <div class="o-h r4 mr20" style="width: 290px">
        <div class="f18 bold lh150 ptb20 b-b mb20">组件列表区</div>
        <comp-group
          v-for="(item, index) in compArr"
          :key="index"
          :title="item.title"
          :list="item.listData"
        ></comp-group>
      </div>

      <div class="f100 o-h r4 f100 ml20 mr20">
        <div class="f18 bold lh150 ptb20 b-b mb20">实时预览区</div>
        <div class="border r4">
          <div class="f20 lh150 ptb10 b-b ml10 mr10">页面</div>
          <draggable
            :style="{minHeight: '150px'}"
            :options="fromOptions"
            class="ptb20 plr20"
            @start="drag=true"
            @end="drag=false"
          ></draggable>
        </div>
      </div>

      <div class="o-h r4 mr20" style="width: 290px">
        <div class="f18 bold lh150 ptb20 b-b mb20">属性配置区</div>
        <div class="flex fd-c ai-c">属性配置区域---待开发</div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import CompGroup from '~/components/CompGroup.vue'
import draggable from 'vuedraggable'

export default {
  components: {
    Logo,
    draggable,
    CompGroup
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
      },
      compArr: [
        {
          title: '表单',
          listData: [{ text: '输入框', ico: 'cube' }]
        },
        {
          title: '表单1',
          listData: [{ text: '输入框2', ico: 'cube' }]
        }
      ]
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
