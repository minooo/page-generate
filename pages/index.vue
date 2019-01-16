<template>
  <div>
    <div class="bg-main c-white plr20 ptb15 f18 bold">页面构造器（v0.0.1）</div>
    <div class="flex plr20">
      <div class="f110 o-h r4 mr20">
        <div class="f24 bold lh150 ptb20 b-b mb20">组件列表区</div>
        <div class="flex fd-c ai-c">
          <draggable
            style="width: 100px"
            class="flex fd-c ai-c ptb20 move"
            @start="onDragStart"
            @end="onDragEnd"
          >
            <span>文本框</span>
          </draggable>

          <div class="plr20 ptb20">
            <span>标题</span>
            <Input v-model="value" placeholder="Enter something..." style="width: 300px"/>
          </div>
        </div>
      </div>

      <div class="f110 o-h r4">
        <div class="f24 bold lh150 ptb20 b-b mb20">实时预览区</div>
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
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import draggable from 'vuedraggable'

export default {
  components: {
    Logo,
    draggable
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
