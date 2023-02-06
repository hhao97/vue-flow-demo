<script setup>
import { Handle, Position } from "@vue-flow/core";
import { NodeResizer } from "@vue-flow/node-resizer";
import { computed, watch } from "vue";
const props = defineProps({
  // resizableNode: {
  //     type: Object,
  //     required: true
  // },
  node: {
    type: Object,
    required: true,
  },
});
// 白板中每创建一个该 node 都会新增一个 watch 可能会有性能问题
watch(props.node, (newV, oldV) => {
  if (newV.selected == true) {
    newV.class = "custom_selected";
  } else {
    newV.class = "li111ne";
  }
});

// const emit = defineEmits(["update:resizableNode"]);

// const customNode = computed({
//   get: () => props.resizableNode,
//   set: (val) => {
//     console.log(val);
//     emit("update:resizableNode", val);
//   },
// });
const customNode = computed(() => {
  return props.node;
});

const sourceHandleStyleB = computed(() => ({
  //  display:"none",
}));
const mouseIn = (e) => {
  props.node.mouseenter = true;
  console.log("mouse in ", props.node.mouseenter);
};
const mouseOut = (e) => {
  props.node.mouseenter = false;
  console.log("mouse out ", props.node.mouseenter);
};
</script>

<template >
  <div @mouseenter="mouseIn" @mouseleave="mouseOut">
    <NodeResizer min-width="100" min-height="30" v-if="customNode.selected" />
    <Handle
      type="source"
      :position="Position.Right"
      :style="sourceHandleStyleB"
      v-if="customNode.selected || props.node.mouseenter"
    />
    <Handle
      type="source"
      :position="Position.Top"
      :style="sourceHandleStyleB"
      v-if="customNode.selected || props.node.mouseenter"
    />
    <Handle
      type="source"
      :position="Position.Left"
      :style="sourceHandleStyleB"
      v-if="customNode.selected || props.node.mouseenter"
    />
    <Handle
      type="target"
      :position="Position.Bottom"
      :style="sourceHandleStyleB"
      v-if="customNode.selected || props.node.mouseenter"
    />

    <div class="content">
        {{customNode.label}}
    </div>
  </div>
</template>

<style scoped>
.content {
  min-width: 100px;
  min-height: 30px;
}
</style>