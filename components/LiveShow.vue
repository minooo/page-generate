<template>
  <div class="f100 o-h r4 f100 ml20 mr20">
    <!-- 头部 -->
    <div class="flex mb20 b-b">
      <div
        :class="`f18 bold lh150 ptb20 f00a pointer mr20 ${viewable ? '' : 'c999'}`"
        @click="viewable = true"
      >实时预览区</div>
      <div
        :class="`f18 bold lh150 ptb20 f00a pointer ${viewable ? 'c999' : ''}`"
        @click="viewable = false"
      >生成JSON</div>
      <draggable
        :style="{minHeight: '10px'}"
        :options="dragOptions"
        v-model="list"
        class="f100 flex jc-c ai-c f16 rel delete"
      />
    </div>
    <!-- 内容 -->
    <div class="page-border r4">
      <draggable
        v-if="viewable"
        :style="{minHeight: '20px'}"
        :options="dragOptions"
        v-model="list"
        class="ptb15 plr15"
      >
        <component
          v-for="(item, index) in list"
          :is="item.comp.name"
          :key="index"
          v-bind="item.comp.prop"
        >{{ item.comp.name }}</component>
      </draggable>

      <div v-else class="ptb15 plr15">
        <pre>{{ listString }}</pre>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import LiveShowList from '~/components/LiveShowList.vue'

export default {
  components: {
    draggable,
    LiveShowList
  },
  data() {
    return {
      viewable: true,
      list: [],
      dragOptions: {
        group: {
          put: true
        },
        animation: 300
      }
    }
  },
  computed: {
    listString() {
      const result = this.list.map(x => x.comp)
      return JSON.stringify(result, null, 2)
    }
  }
}
</script>

<style scoped>
.delete:before {
  display: block;
  position: absolute;
  content: '删除组件拖至此处即可';
  color: red;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
</style>
