<template>
  <div>
    <div class="bg-main c-white plr20 ptb15 f18 bold">页面构造器</div>
    <div class="flex plr20">
      <div class="f110 o-h r4 mr20">
        <div class="f24 bold lh150 ptb20 b-b mb20">生成的页面</div>
        <div class="border r4">
          <div class="f20 lh150 ptb10 b-b ml10 mr10">页面</div>
          <div :style="{minHeight: '150px'}"></div>
        </div>
      </div>
      <div class="f110 o-h r4">
        <div class="f24 bold lh150 ptb20 b-b mb20">拖拽下面的组件到左侧</div>
        <div class="flex fd-c ai-c">
          <div>
            <span>标题</span>
            <Input v-model="value" placeholder="Enter something..." style="width: 300px"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      value: ''
    }
  }
}
</script>

<style>
</style>
