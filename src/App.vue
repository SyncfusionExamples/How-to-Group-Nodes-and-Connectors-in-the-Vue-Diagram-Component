<template>
  <div class="container">
    <ejs-button class="button" @click="addChildNodeToGroup">Add Child Node to Group</ejs-button>
    <ejs-button class="button" @click="ungroup">Ungroup</ejs-button>
    <ejs-button class="button" @click="updateGroup">Update Group</ejs-button>
  </div>
  <ejs-diagram ref="diagramObject" :width="width" :height="height" :nodes="nodes" :connectors="connectors"></ejs-diagram>
</template>
<script>

let diagramInstance;

let connectors = [
  {
    id: 'connector1',
    sourceID: 'node1',
    targetID: 'node2'
  },
  {
    id: 'connector2',
    sourceID: 'node2',
    targetID: 'node3'
  },
  {
    id: 'connector3',
    sourceID: 'node3',
    targetID: 'node1'
  }
];

let nodes = [
  {
    id: "node1",
    offsetX: 375,
    offsetY: 130,
    height: 60,
    width: 150,
    annotations: [ { content: "Node 1" } ]
  },
  {
    id: "node2",
    offsetX: 675,
    offsetY: 130,
    height: 60,
    width: 150,
    annotations: [ { content: "Node 2" } ]
  },
  {
      id: "node3",
      offsetX: 525, offsetY: 270,
      height: 60, width: 150,
      annotations: [{ content: "Node 3" }]
  },
  {
      id: "node4",
      offsetX: 525, offsetY: 370,
      height: 60, width: 150,
      annotations: [{ content: "Node 4" }]
  }
];

let group = {
    id: 'group1',
    children: ['node1', 'node2', 'connector1', 'connector2', 'connector3', 'node3'],
    padding: { left:20, right:20, top:20, bottom:20 },
    style: { fill:'Orange', strokeColor: 'Black', strokeWidth:2 },
    annotations: [{ content: 'Group Node'}]
  };

  let nestedGroup = {
    id: 'nestedGroup1',
    children: ['group1', 'node4'],
    padding: { left:20, right:20, top:20, bottom:20 },
    style: { fill:'Blue', strokeColor: 'Black', strokeWidth:2 },
    annotations: [{ content: 'Nested Group Node'}]
  };


import { DiagramComponent } from '@syncfusion/ej2-vue-diagrams';
import { ButtonComponent } from '@syncfusion/ej2-vue-buttons';

export default {
  components: {
    'ejs-diagram': DiagramComponent,
    'ejs-button': ButtonComponent
  },
  data: function () {
    return {
      width: '1102px',
      height: '602px',
      nodes: nodes,
      connectors: connectors
    };
  },
  methods: {
    addChildNodeToGroup(){
      diagramInstance.addChildToGroup(group, 'node3');
    },
    ungroup(){
      diagramInstance.unGroup();
    },
    updateGroup(){
      diagramInstance.nodes[3].offsetX = 300;
      diagramInstance.nodes[3].offsetY = 300;
    }
  },
  mounted: function(){
    diagramInstance = this.$refs.diagramObject.ej2Instances;
    diagramInstance.add(group);
    diagramInstance.add(nestedGroup);
  }
};
</script>

<style>
@import "../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-buttons/styles/material.css";

.container {
  text-align: left;
  margin-bottom: 10px;
}

.button{
  margin-right: 10px;
}
</style>