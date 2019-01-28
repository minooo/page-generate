<template>
  <div class="o-h r4" style="width: 260px">
    <div class="f18 bold lh150 ptb20 b-b mb20">属性配置区</div>
    <div class="plr15 ptb15 border">
      <Form :model="curlist" label-position="top">
        <template v-if="curlist.tag === 'f-input'">
          <FormItem label="标题">
            <Input :maxlength="10" v-model="curlist.prop.label"/>
          </FormItem>
          <FormItem label="输入框类型选择">
            <Select v-model="curlist.comp[0].prop.type">
              <Option value="text">输入框</Option>
              <Option value="textarea">文本域</Option>
              <Option value="password">密码</Option>
              <Option value="url">URL</Option>
              <Option value="email">Email</Option>
            </Select>
          </FormItem>
          <FormItem v-if="curlist.comp[0].prop.type === 'textarea'" label="文本域行数选择">
            <Input v-model="curlist.comp[0].prop[':rows']"/>
          </FormItem>
          <FormItem label="输入框样式设置">
            <Input v-model="curlist.comp[0].prop.style"/>
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
                  <Input :maxlength="10" v-model="item.prop.label" placeholder="label"></Input>
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
        <template v-else-if="curlist.tag === 'f-select'">
          <FormItem label="标题">
            <Input :maxlength="10" v-model="curlist.prop.label"/>
          </FormItem>
          <FormItem label="子选项设置 value/label">
            <FormItem v-for="(item, index) in curlist.comp[0].comp" :key="index">
              <Row>
                <Col span="12">
                  <Input :maxlength="10" v-model="item.prop.value" placeholder="val" class="mb10"></Input>
                  <Input :maxlength="10" v-model="item.prop.label" placeholder="label"></Input>
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
      const isCheckbox = this.curlist.tag === 'f-checkbox'
      const isSelect = this.curlist.tag === 'f-select'
      if (isCheckbox) {
        this.curlist = {
          ...this.curlist,
          comp: [{ name: 'CheckboxGroup', comp }]
        }
      } else if (isSelect) {
        this.curlist = {
          ...this.curlist,
          comp: [{ name: 'Select', comp }]
        }
      }
    },
    handleAdd: function() {
      const comp = [...this.curlist.comp[0].comp]
      const isCheckbox = this.curlist.tag === 'f-checkbox'
      const isSelect = this.curlist.tag === 'f-select'
      if (isCheckbox) {
        comp.push({ name: 'Checkbox', prop: { label: 'Item' } })
        this.curlist = {
          ...this.curlist,
          comp: [{ name: 'CheckboxGroup', comp }]
        }
      } else if (isSelect) {
        comp.push({
          name: 'Option',
          prop: { value: 'value值', label: 'label值' }
        })
        this.curlist = {
          ...this.curlist,
          comp: [{ name: 'Select', comp }]
        }
      }
    }
  }
}
</script>
