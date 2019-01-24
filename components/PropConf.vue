<template>
  <div class="o-h r4" style="width: 260px">
    <div class="f18 bold lh150 ptb20 b-b mb20">属性配置区</div>
    <div class="plr15 ptb15 border">
      <Form :model="curlist" label-position="top">
        <template v-if="curlist.tag === 'f-input'">
          <FormItem label="标题">
            <Input v-model="curlist.prop.label"/>
          </FormItem>
          <FormItem label="占位内容">
            <Input v-model="curlist.comp[0].prop.placeholder"/>
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
      console.log('on lala', param)
      app.curlist = JSON.parse(JSON.stringify(param.item))
      console.log('kk', this, this.curlist)
      app.index = param.index
    })
  }
}
</script>
