<template>
  <div>
   <el-tree
     :expand-on-click-node="false"
     :highlight-current="true"
     ref="tree"
     :data="data"
     :node-key="nodeKey"
     :current-node-key="currentNodeKey"
     :default-expanded-keys="defaultExpandedKeys"
     @node-click="nodeClick"
     @current-change="currentChange"
     @node-collapse="nodeCollapse"
   >
   </el-tree>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Watch } from 'vue-property-decorator'

@Component({})
export default class OwnTree extends Vue {
  @Prop({ default: 'id' }) nodeKey!: string
  @Prop() data!: Array<any>
  @Prop() currentNodeKey!: string|number
  @Prop() instance!: any
  @Prop({ default: [] }) defaultExpandedKeys!: Array<string|number>
  @Prop({ default: false }) expandOnClickNode!: boolean
  @Prop({ default: true }) highlightCurrent!: boolean

  @Watch('currentNodeKey')
  handleNodeChange (val: string| number, old: any) {
    const ref = this.$refs.tree as any
    if (val === old || old !== ref.getCurrentKey()) return
    const node = ref.getNode(val)
    ref.setCurrentKey(val)
    ref.setCurrentNode(node.data)
    let parent = node
    while (parent.parent) {
      parent = parent.parent
      parent.expanded = true
    }
  }

  created () {
  }

  nodeClick (...arg: any) {
    console.log(arg[1])
    this.$emit('update:current-node-key', arg[0].id)
    this.$emit('node-click', ...arg)
  }

  currentChange (...arg: any) {
    console.log('节点变化')
    this.$emit('current-change', ...arg)
  }

  nodeCollapse (...arg: any) {
    console.log(this.expandedKeys)
  }
}
</script>

<style scoped>

</style>
