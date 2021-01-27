<template>
  <div class="home">
   <Own-tree
     :data="treeData"
     :current-node-key.sync="currentNode"
     :default-expanded-keys="expandedKeys"
     @node-click="nodeClick"
   ></Own-tree>
    <el-button @click="change">改变</el-button>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
import OwnTree from '@/components/OwnTree.vue'

@Component({
  components: {
    OwnTree
  }
})
export default class Home extends Vue {
  keys = ['6', '8']
  treeData = [{
    id: '1',
    label: '一级 1',
    children: [{
      id: '4',
      label: '二级 1-1',
      children: [{
        id: '9',
        label: '三级 1-1-1'
      }, {
        id: '10',
        label: '三级 1-1-2'
      }]
    }]
  }, {
    id: '2',
    label: '一级 2',
    children: [{
      id: '5',
      label: '二级 2-1'
    }, {
      id: '6',
      label: '二级 2-2'
    }]
  }, {
    id: '3',
    label: '一级 3',
    children: [{
      id: '7',
      label: '二级 3-1'
    }, {
      id: '8',
      label: '二级 3-2'
    }]
  }]

  nodeKey = 'id'
  currentNode = '6'
  expandedKeys = ['6']

  change () {
    this.currentNode = '9'
  }

  nodeClick (data: any) {

  }

  nodeExpand () {
    console.log(this.keys)
  }
}
</script>
