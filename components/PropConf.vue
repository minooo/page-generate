<template>
  <div class="o-h r4" style="width: 260px">
    <div class="f18 bold lh150 ptb20 b-b mb20">属性配置区</div>
    <div class="plr15 ptb15 border">
      <Form :model="curlist" label-position="top">
        <template v-if="curlist.tag === 'f-input'">
          <FormItem label="标题">
            <Input :maxlength="10" v-model="curlist.prop.label"/>
          </FormItem>
          <FormItem label="占位内容">
            <Input :maxlength="10" v-model="curlist.comp[0].prop.placeholder"/>
          </FormItem>
        </template>
        <template v-else-if="curlist.tag === 'f-checkbox'">
          <FormItem label="标题">
            <Input :maxlength="10" v-model="curlist.prop.label"/>
          </FormItem>
          <FormItem label="子选项">
            <FormItem v-for="(item, index) in curlist.comp[0].comp" :key="index">
              <Row>
                <Col span="12">
                  <Input :maxlength="10" v-model="item.prop.label" placeholder="Enter something..."></Input>
                </Col>
                <Col span="4" offset="1">
                  <Button @click="handleRemove(index)">删除</Button>
                </Col>
              </Row>
              <div class="mb10"/>
            </FormItem>
            <Row>
              <Col span="12">
                <Button type="dashed" @click="handleAdd" icon="plus-round">添加子项</Button>
              </Col>
            </Row>
          </FormItem>
        </template>
      </Form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      curlist: {},
      index: -1
    }
  },
  watch: {
    curlist: {
      handler: function(val, oldval) {
        const app = this
        this.$root.$emit('changelist', {
          curlist: [app.curlist],
          index: app.index
        })
      },
      deep: true
    }
  },
  mounted() {
    const app = this
    this.$root.$on('curlist', function(param) {
      app.curlist = JSON.parse(JSON.stringify(param.item))
      app.index = param.index
    })
  },
  methods: {
    handleRemove: function(index) {
      const comp = [...this.curlist.comp[0].comp]
      comp.splice(index, 1)
      this.curlist = {
        ...this.curlist,
        comp: [{ name: 'CheckboxGroup', comp }]
      }
    },
    handleAdd: function() {
      const comp = [...this.curlist.comp[0].comp]
      comp.push({
        name: 'Checkbox',
        prop: { label: 'Item' }
      })

      this.curlist = {
        ...this.curlist,
        comp: [{ name: 'CheckboxGroup', comp }]
      }
    }
  }
}
</script>
