<template>
  <div class="f100 o-h r4 f100 ml20 mr20">
    <!-- 头部 -->
    <div class="flex mb20 b-b">
      <div
        :class="`f18 bold lh150 ptb20 f00a pointer mr20 us-n ${viewable ? '' : 'c999'}`"
        @click="viewable = true"
      >实时预览区</div>
      <div
        :class="`f18 bold lh150 ptb20 f00a pointer us-n ${viewable ? 'c999' : ''}`"
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
      <Form v-if="viewable" :label-width="80">
        <draggable
          :style="{minHeight: '20px'}"
          :options="dragOptions"
          v-model="list"
          class="ptb15 plr15"
        >
          <div v-if="list.length === 0">将组件拖放到这里</div>
          <template v-for="(item, index) in list" v-else>
            <div v-for="x in item.comp" :key="$uuid.v4()" @click="onComp(x, index)">
              <component :is="x.name" v-bind="x.prop">
                <template v-if="x.comp">
                  <component v-for="m in x.comp" :key="$uuid.v4()" :is="m.name" v-bind="m.prop">
                    <template v-if="m.comp">
                      <component
                        v-for="n in m.comp"
                        :key="$uuid.v4()"
                        :is="n.name"
                        v-bind="n.prop"
                      />
                    </template>
                  </component>
                </template>
              </component>
            </div>
          </template>
        </draggable>
      </Form>
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
  },
  mounted() {
    const app = this
    this.$root.$on('changelist', function(param) {
      const { curlist, index } = param
      app.list.splice(index, 1, { ...app[index], comp: curlist })
    })
  },
  methods: {
    onComp: function(item, index) {
      this.$root.$emit('curlist', { item, index })
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
