<template>
  <div>
    <div class="bg-main c-white plr20 ptb15 f18 bold">页面构造器（v0.0.1）</div>
    <div class="flex plr20">
      <!-- 组件列表区 -->
      <div class="o-h r4 mr20" style="width: 260px">
        <div class="f18 bold lh150 ptb20 b-b mb20">组件列表区</div>
        <comp-group
          v-for="(item, index) in compArr"
          :key="index"
          :title="item.title"
          :list="item.list"
        ></comp-group>
      </div>

      <!-- 实时预览区 -->
      <div class="f100 o-h r4 f100 ml20 mr20">
        <div class="flex mb20 b-b">
          <div class="f18 bold lh150 ptb20 f00a" @click="giveData">实时预览区</div>
          <draggable
            :style="{minHeight: '10px'}"
            :options="dragOptions"
            v-model="list"
            class="f100 flex jc-c ai-c f16 rel delete"
            @change="onChange"
          ></draggable>
        </div>

        <div class="page-border r4">
          <draggable
            :style="{minHeight: '20px'}"
            :options="dragOptions"
            v-model="list"
            class="ptb15 plr15"
            @change="onChange"
          >
            <component
              v-for="(item, index) in list"
              :key="index"
              :is="item.comp.name"
            >{{ item.comp.name }}</component>
          </draggable>
        </div>
      </div>

      <!-- JSON -->
      <div class="o-h r4 mr20" style="width: 290px">
        <div class="f18 bold lh150 ptb20 b-b mb20">JSON</div>
        <div class="ptb15 plr15">
          <pre>{{ listString }}</pre>
        </div>
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
      list: [],
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
  },
  computed: {
    listString() {
      const result = this.list.map(x => x.comp)
      return JSON.stringify(result, null, 2)
    }
  },
  mounted() {
    this.$on('onChoose', function(msg) {
      console.log('choose')
    })
  },
  methods: {
    giveData: function() {
      console.log('list', this.list)
    },
    onChange: function(e) {
      console.log('change', e)
    }
  }
}
</script>

<style>
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
