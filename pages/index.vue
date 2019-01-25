<template>
  <div>
    <div class="bg-main c-white plr20 ptb15 f18 bold">页面构造器（v0.0.2）</div>
    <div class="flex plr20">
      <!-- 组件列表区 -->
      <comp/>

      <!-- 实时预览区 -->
      <live-show/>

      <!-- 属性配置区 -->
      <prop-conf/>
    </div>
  </div>
</template>

<script>
import Comp from '~/components/Comp.vue'
import LiveShow from '~/components/LiveShow.vue'
import PropConf from '~/components/PropConf.vue'

export default {
  components: {
    Comp,
    LiveShow,
    PropConf
  }
}
</script>

<style>
</style>
